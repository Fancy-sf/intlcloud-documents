## Overview
The Go SDK provides APIs for getting pre-signed request URLs. This document provides samples for detailed directions.

>?
> - We recommend you use a temporary key to generate a pre-signed URL for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [principle of least privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you need to use a permanent key to generate a pre-signed URL, you are advised to limit the permission of the permanent key to uploads and downloads only to avoid risks.
> 

## Getting Pre-signed Request URL 

```go
func (s *ObjectService) GetPresignedURL(ctx context.Context, httpMethod, name, ak, sk string, expired time.Duration, opt interface{}, signHost ...bool) (*url.URL, error)
```

#### Parameter description

```go
type PresignedURLOptions struct {
    Query      *url.Values
    Header     *http.Header
}
```

| Parameter | Type | Description |
| ------------------ | ---------------------------- | ------------------------------- |
| httpMethod | string | HTTP request method |
| name | string | HTTP request path, i.e., object key |
| ak             | string                       | SecretId                    |
| sk               | string                       | SecretKey         |
| expired | time.Duration | Validity period of the signature |
| opt    | interface{} | Extension. We recommend you enter parameters of the \*PresignedURLOptions type or `nil`. |
| PresignedURLOptions | struct | Request parameters and headers to include in the signature |
| Query | struct | Request parameters to include in the signature |
| Header | struct | Request headers to include in the signature |
| signHost | bool | Whether to include the `host` header in the signature. The default value is `true`. You can also choose not to include the `host` header in the signature, but the request may fail or vulnerabilities may occur. This parameter is optional. |

## Generating Pre-Signed URL with Permanent Key

#### Sample requests for upload

[//]: # ".cssg-snippet-get-presign-upload-url"
```go
package main

import (
        "context"
        "github.com/tencentyun/cos-go-sdk-v5"
        "net/http"
        "net/url"
        "os"
        "strings"
        "time"
)

func main() {
        // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        // Replace it with your `region`, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information on regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
        u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
        b := &cos.BaseURL{BucketURL: u}
        client := cos.NewClient(b, &http.Client{
                Transport: &cos.AuthorizationTransport{
                        // Get the key from environment variables.
                        // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
                        SecretID: os.Getenv("SECRETID"),
                        // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
                        SecretKey: os.Getenv("SECRETKEY"),
                },
        })

        ak := "SECRETID"
        sk := "SECRETKEY"

        name := "exampleobject"
        ctx := context.Background()
        f := strings.NewReader("test")

        // 1. Upload the object in the standard method.
        _, err := client.Object.Put(ctx, name, f, nil)
        if err != nil {
                panic(err)
        }
        // Get the pre-signed URL.
        presignedURL, err := client.Object.GetPresignedURL(ctx, http.MethodPut, name, ak, sk, time.Hour, nil)
        if err != nil {
                panic(err)
        }
        // 2. Upload the object through a pre-signed URL.
        data := "test upload with presignedURL"
        f = strings.NewReader(data)
        req, err := http.NewRequest(http.MethodPut, presignedURL.String(), f)
        if err != nil {
                panic(err)
        }
        // You can configure request headers by yourself.
        req.Header.Set("Content-Type", "text/html")
        _, err = http.DefaultClient.Do(req)
        if err != nil {
                panic(err)
        }
}
```

#### Sample requests for download

[//]: # ".cssg-snippet-get-presign-download-url"
```go
package main

import (
        "bytes"
        "context"
        "errors"
        "github.com/tencentyun/cos-go-sdk-v5"
        "io/ioutil"
        "net/http"
        "net/url"
        "os"
        "time"
)

func main() {
        // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        // Replace it with your `region`, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information on regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
        u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
        b := &cos.BaseURL{BucketURL: u}
        client := cos.NewClient(b, &http.Client{
                Transport: &cos.AuthorizationTransport{
                        // Get the key from environment variables.
                        // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
                        SecretID: os.Getenv("SECRETID"),
                        // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
                        SecretKey: os.Getenv("SECRETKEY"),
                },
        })

        ak := "SECRETID"
        sk := "SECRETKEY"
        name := "exampleobject"
        ctx := context.Background()
        // 1. Download the object in the standard method.
        resp, err := client.Object.Get(ctx, name, nil)
        if err != nil {
                panic(err)
        }
        bs, _ := ioutil.ReadAll(resp.Body)
        resp.Body.Close()
        // Get the pre-signed URL.
        presignedURL, err := client.Object.GetPresignedURL(ctx, http.MethodGet, name, ak, sk, time.Hour, nil)
        if err != nil {
                panic(err)
        }
        // 2. Download the object through a pre-signed URL
        resp2, err := http.Get(presignedURL.String())
        if err != nil {
                panic(err)
        }
        bs2, _ := ioutil.ReadAll(resp2.Body)
        resp2.Body.Close()
        if bytes.Compare(bs2, bs) != 0 {
                panic(errors.New("content is not consistent"))
        }
}
```

## Generating Pre-Signed URL with Temporary Key

#### Sample requests for upload
```go
package main

import (
    "context"
    "fmt"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
    "time"
    "strings"
)
// You can use tags to put the request parameters or request headers in the signature.
type URLToken struct {
	SessionToken string `url:"x-cos-security-token,omitempty" header:"-"`
}

func main() {
	// Replace it with your temporary key.
	tak := os.Getenv("SECRETID")
	tsk := os.Getenv("SECRETKEY")
	token := &URLToken{
		SessionToken: "<token>",
	}
	u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
	b := &cos.BaseURL{BucketURL: u}
	c := cos.NewClient(b, &http.Client{})

	name := "exampleobject"
	ctx := context.Background()

	// Method 1. Use `PresignedURLOptions` to configure `x-cos-security-token`.
	// You can add request parameters and request headers through `PresignedURLOptions`.
	opt := &cos.PresignedURLOptions{
		Query:  &url.Values{},
		Header: &http.Header{},
	}
	opt.Query.Add("x-cos-security-token", "<token>")
	// Get the pre-signed URL.
	presignedURL, err := c.Object.GetPresignedURL(ctx, http.MethodPut, name, tak, tsk, time.Hour, opt)
	if err != nil {
		fmt.Printf("Error: %v\n", err)
		return
	}
	// Upload the object through a pre-signed URL.
	data := "test upload with presignedURL"
	f := strings.NewReader(data)
	req, err := http.NewRequest(http.MethodPut, presignedURL.String(), f)
	if err != nil {
		fmt.Printf("Error: %v\n", err)
	}
	_, err = http.DefaultClient.Do(req)
	if err != nil {
		fmt.Printf("Error: %v\n", err)
	}	

	// Method 2. Use tags to configure `x-cos-security-token`.
	// Get the pre-signed URL.
	presignedURL, err = c.Object.GetPresignedURL(ctx, http.MethodPut, name, tak, tsk, time.Hour, token)
	if err != nil {
		fmt.Printf("Error: %v\n", err)
		return
	}
	f = strings.NewReader(data)
	req, err = http.NewRequest(http.MethodPut, presignedURL.String(), f)
	if err != nil {
		fmt.Printf("Error: %v\n", err)
	}
	_, err = http.DefaultClient.Do(req)
	if err != nil {
		fmt.Printf("Error: %v\n", err)
	}	
}
```

#### Sample requests for download

```go
package main

import (
    "context"
    "fmt"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
    "time"
)
// You can use tags to put the request parameters or request headers in the signature.
type URLToken struct {
	SessionToken string `url:"x-cos-security-token,omitempty" header:"-"`
}

func main() {
	// Replace it with your temporary key.
	tak := os.Getenv("SECRETID")
	tsk := os.Getenv("SECRETKEY")
	token := &URLToken{
		SessionToken: "<token>",
	}
	u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
	b := &cos.BaseURL{BucketURL: u}
	c := cos.NewClient(b, &http.Client{})

	name := "exampleobject"
	ctx := context.Background()

    // Method 1. Use `PresignedURLOptions` to configure `x-cos-security-token`.
    // You can add request parameters and request headers through `PresignedURLOptions`.
	opt := &cos.PresignedURLOptions{
		Query:  &url.Values{},
		Header: &http.Header{},
	}
	opt.Query.Add("x-cos-security-token", "<token>")
	// Get the pre-signed URL.
	presignedURL, err := c.Object.GetPresignedURL(ctx, http.MethodGet, name, tak, tsk, time.Hour, opt)
	if err != nil {
		fmt.Printf("Error: %v\n", err)
		return
	}
	// Access the object through the pre-signed URL.
	resp, err := http.Get(presignedURL.String())
	if err != nil {
		fmt.Printf("Error: %v\n", err)
	}
	defer resp.Body.Close()
	fmt.Println(presignedURL.String())
	fmt.Printf("resp:%v\n", resp)

	// Method 2. Use tags to configure `x-cos-security-token`.
	// Get the pre-signed URL.
	presignedURL, err = c.Object.GetPresignedURL(ctx, http.MethodGet, name, tak, tsk, time.Hour, token)
	if err != nil {
		fmt.Printf("Error: %v\n", err)
		return
	}
	// Access the object through the pre-signed URL.
	resp, err = http.Get(presignedURL.String())
	if err != nil {
		fmt.Printf("Error: %v\n", err)
	}
	defer resp.Body.Close()
	fmt.Println(presignedURL.String())
	fmt.Printf("resp:%v\n", resp)
}
```

## Sample of Generating Pre-Signed URL for Custom Domain Name
```go
package main

import (
    "context"
    "fmt"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
    "time"
)
func main() {
    // Replace it with your key.
    tak := os.Getenv("SECRETID")
    tsk := os.Getenv("SECRETKEY")
    // Change it to the custom domain.
    u, _ := url.Parse("https://<custom domain name>")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{})

    name := "exampleobject"
    ctx := context.Background()

    // Get the pre-signed URL.
    presignedURL, err := c.Object.GetPresignedURL(ctx, http.MethodGet, name, tak, tsk, time.Hour, nil)
    if err != nil {
        fmt.Printf("Error: %v\n", err)
        return
    }
    // Access the object through the pre-signed URL.
    resp, err := http.Get(presignedURL.String())
    if err != nil {
        fmt.Printf("Error: %v\n", err)
    }
    defer resp.Body.Close()
    fmt.Println(presignedURL.String())
    fmt.Printf("resp:%v\n", resp)
}
```

## Adding Request Parameter or Header
```go
package main

import (
    "context"
    "fmt"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
    "time"
)
func main() {
	// Replace it with your temporary key.
	tak := os.Getenv("SECRETID")
	tsk := os.Getenv("SECRETKEY")
	u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
	b := &cos.BaseURL{BucketURL: u}
	c := cos.NewClient(b, &http.Client{})

	name := "exampleobject"
	ctx := context.Background()

	// You can add request parameters and request headers through `PresignedURLOptions`.
	opt := &cos.PresignedURLOptions{
	    // HTTP request parameters, which should be the same as those passed to the actual request. This can prevent users from tampering with the HTTP request parameters.
		Query:  &url.Values{},
		// HTTP request headers, which should be included in the actual request. This can prevent users from tampering with the HTTP request headers that are signed here.
		Header: &http.Header{},
	}
	// Add request parameters. The returned pre-signed URL will include the added parameters.
	opt.Query.Add("x-cos-security-token", "<token>")
	// Add request headers. The returned pre-signed URL only sets the request headers to the signature. Therefore, you still need to set the headers when making requests.
	opt.Header.Add("Content-Type", "text/html")

	// The SDK includes the `host` header in the signature by default. If the `signHost` parameter is not passed in or `SignHost` is `true`, the `host` header is included in the signature.
	// If `signHost` is `false`, the `host` header is not included in the signature, which may lead to request failure or security vulnerabilities.
	var signHost bool = true
	// Get the pre-signed URL with the signature containing `host`.
	presignedURL, err := c.Object.GetPresignedURL(ctx, http.MethodPut, name, tak, tsk, time.Hour, opt, signHost)
	if err != nil {
		fmt.Printf("Error: %v\n", err)
		return
	}
	// Access the object through the pre-signed URL.
	req, _ := http.NewRequest(http.MethodPut, presignedURL.String(), strings.NewReader("test"))
	// Set headers when making requests.
	req.Header.Set("Content-Type", "text/html")
	resp, err := http.DefaultClient.Do(req)
	if err != nil {
		fmt.Printf("Error: %v\n", err)
	}
	defer resp.Body.Close()
	fmt.Println(presignedURL.String())
	fmt.Printf("resp:%v\n", resp)
}
```


