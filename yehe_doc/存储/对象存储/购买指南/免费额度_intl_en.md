## Overview
COS offers a limited free tier resource pack to all new users (i.e., users activating COS for the first time) to deduct the fees incurred by data stored in the **STANDARD** storage class, as detailed below: 

| Object | Free Tier | Validity |
| -------- | ----------------- | ------ |
| New user | 50 GB STANDARD storage usage | 6 months (180 days) |

>?The storage capacity is calculated in binary, for example, 1 TB = 1024 GB.

## Applicable Regions

The free tier is only applicable to **public cloud regions**. For more information on regions, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).

The free tier offered by COS can be used to deduct only **STANDARD storage usage** as detailed below. For more information, see [Traffic Fees](https://intl.cloud.tencent.com/document/product/436/33776).

>!
> - The free tier cannot be used to deduct billable items **other than STANDARD storage usage**, such as STANDARD_IA storage usage, ARCHIVE storage usage, requests, and traffic. For more information, see [Billable Items](https://www.tencentcloud.com/document/product/436/40096).
> - If your service is suspended due to violations or overdue payment, you will not be eligible for the free tier even within its validity period before the service is resumed.
> 

<table>
   <tr>
      <th>Fees</th>
      <th>Billable Item</th>
      <th>Available Free Tier</th>
   </tr>
   <tr>
      <td rowspan="5">Storage usage fees</td>
      <td>STANDARD storage usage</td>
      <td>Yes.<br>New users are entitled to a free tier of 50 GB STANDARD storage usage for 6 months (180 days).</td>
   </tr>
   <tr>
      <td>STANDARD_IA storage usage</td>
      <td rowspan="8">No.<br>The free tier cannot be used to deduct billable items other than <strong>STANDARD storage usage</strong>.</br></td>
   </tr>
   <tr>
      <td>INTELLIGENT TIERING storage usage</td>
   </tr>
   <tr>
      <td>ARCHIVE storage usage</td>
   </tr>
   <tr>
      <td>DEEP ARCHIVE storage usage</td>	   
   </tr>
   <tr>
      <td>Request fees</td>
      <td>Requests</td>
   </tr>
   <tr>
      <td>Data retrieval fees</td>
      <td>Data retrieval</td>
   </tr>
   <tr>
      <td rowspan="1">Traffic fees</td>
      <td>Public network downstream traffic, CDN origin-pull traffic, cross-region replication traffic, and global acceleration traffic</td>
   </tr>
   <tr>
	     <td rowspan="1">Management feature fees</td>
       <td>Inventory, extraction, batch operation, and object tagging</td>
   </tr>
</table>



## Examples

> ?
> - For more information on billing after the free tier term ends, see [Billing Examples](https://intl.cloud.tencent.com/document/product/436/6241).
> - Prices in the following examples are for reference only. For the actual prices, see [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).
> 


Assume that user A activated the COS service on March 10, 2019, uploaded 50 GB of files to the STANDARD storage class in Beijing region on March 16 generating 100 requests, and downloaded 10 GB of data over the public network on March 20 generating 100 requests. Apart from these operations, user A did not perform any other operations before the end of September.


| Time | Description | Unit Price | Volume | Fees (USD) |
|-----|  -----|   -----|----|   -----|
| March 10, 2019 | User A received a monthly free tier of 50 GB STANDARD storage usage valid for 6 months (180 days). | - | - | Free of charge |
| March 17–September 5, 2019 | Starting from March 17, 2019, the STANDARD storage usage fees were settled daily. As user A had a free tier of 50 GB STANDARD storage usage valid between March 10 and September 5, 2019 (180 days), there were no charges. | - | - | Free of charge |
| March 17, 2019 | The fees for 100 STANDARD requests were settled. | 0.024 USD/10,000 requests | 100 requests | 0.024 * 100 / 10000 = 0.00024 USD |
| March 21, 2019 | The fees for 10 GB public network downstream traffic were settled. | 0.1 USD/GB | 10 GB | 0.1 * 10 = 1 USD |
| March 21, 2019 | The fees for 100 STANDARD requests were settled. | 0.01 USD/10,000 requests | 100 requests | 0.01 * 100 / 10000 = 0.0001 USD |
| September 6, 2019 | User A's free tier expired on September 6, 2019, so the storage usage from September 6 to September 30, 2019 (25 days) became pay-as-you-go. Fees for 50 GB STANDARD storage usage were settled daily. | 0.024 USD/GB/month | 50 GB | 0.024 / 30 * 50 * 25 = 1 USD |



## Claim and Query

After you sign up for a Tencent Cloud account as instructed in [Signing Up](https://intl.cloud.tencent.com/document/product/378/17985) and log in to the [COS console](https://console.cloud.tencent.com/cos5) to activate the COS service, the system will automatically issue the free tier to your account.

## Validity Period

The **free tier** is valid for 6 months (180 days) after the activation of your COS service.

For example, if you activated COS at 17:13:14 on March 10, 2019, and assume that 6 months is equal to 180 days, then the free tier would cover your STANDARD storage usage between March 10 and September 5, 2019.

## Billing Sequence

During the free tier term, you may still be charged for other fees, such as request fees and traffic fees. Therefore, the billing sequence varies by scenario.

- By default, the system adopts the **pay-as-you-go** billing mode for bill settlement.
- If you are eligible for the free tier of STANDARD storage usage, then your bills will be settled in the order of **free tier** > **pay-as-you-go billing**, that is, you will be charged in a pay-as-you-go manner for the usage in excess of the free tier.



## Questions

If you have any questions about the free tier or your bills, see [Billing](https://intl.cloud.tencent.com/document/product/436/10373) or [contact us](https://www.tencentcloud.com/contact-us).
