---
layout: default
title: Manage Subscriptions to Domo Listings
parent: Software
---

# Manage Subscriptions to Domo Listings
{: .no_toc }

Apr 19, 2023 ∙ Knowledge Base Article
{: .fs-5 : .fw-300 }

{:  .about }
>As a technical writer intern at Domo, I created this article about managing subscriptions to listings on their BI platform, which provides data integration, visualization, and analysis tools.

You can subscribe to certain Appstore listings with a monthly payment. After you make the initial payment, anyone in your company's Domo instance can install and use the listing. You can also cancel your subscription at any time.

This article describes how to create and manage subscriptions to listings in the following topics:

- TOC
{:toc}

## Subscribe to a listing

1.  Select **Appstore** from the navigation header.
2.  In the side panel of the Appstore, select <img src="https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006uVqy" width="20"> **Search**. 

    ![Search Apps](https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006uW1D)  

    The **Search Apps** page opens.  
3.  Under the **Price** Quick Filter, select the **Monthly** checkbox. There are additional Quick Filters to sort the listings by component, category, publisher name, and data source.  

    All listings that require a monthly payment and match any other Quick Filters display.  
      
    ![Monthly payment listings](https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006uc0D)  
4.  Select a subscription listing to open its Details page.  
5.  Review the listing details, then select **Subscribe Now**.  
      
    ![Subscribe Now](https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006ubcV)  

    You are redirected to Stripe to complete the first payment.  
6.  On the Stripe payment page, complete the **Card information**, **Name on card**, and **Country or region** fields. These fields are required to enable the **Subscribe** button.  
      
    {:  .note }
    >The **Email** field automatically populates with the email associated with your Domo account.
 
7.  (Optional) Select the **Save my info for 1-click checkout with Link** checkbox to reuse your payment information for future transactions. If you select this checkbox, you must also enter your phone number to enable the **Subscribe** button.  
8.  Select **Subscribe** to charge your card for the first subscription payment.  
      
    ![Subscribe](https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006ubck)

If the payment is successful, you are redirected to the **Creating App** modal in Domo. Select **Notify Me** to be notified when your listing is ready for use.  

<img src="https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006ucUS" alt="GIF" width="400">
  
After Domo creates your listing, your newly subscribed listing opens in a new page.

## View your subscriptions

To view a list with details about each of your subscriptions, follow these steps:

1.  Select **Appstore** from the navigation header.
2.  In the side panel of the Appstore, select <img src="https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006uVox" width="20"> **Installed Apps**.  

    ![Installed Apps.png](https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006uW1N)  

    The **Installed Apps** page opens.       
3.  Select **Appstore Purchases** to view all of the listings you and others in your company have purchased.  
      
    ![image.png](https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006ubzk)  
4.  <a id="purchased-by"></a>In the search bar, select <img src="https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006uVyx" width="20"> **Add filter** > **Purchased by** > _**Your Name**_, then repeat for **Purchase type** > **Subscription**.  
      
    ![Add Filter GIF](https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006uXZf)

Your subscriptions display in a list with the following details:

![Subscription list](https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006uc08)

| Detail      | Description |
| ----------- | ----------- |
| Listing      | The name of the listing. Selecting it takes you to the listing Details page.       |
| Purchaser   | The user who purchased the subscription, which is only you in this case. To view subscriptions purchased by others in your company, select a different user from the [**Purchased by**](#purchased-by) list.        |
|Next Payment   | The next due date for the monthly subscription. If the subscription has been canceled, **N/A** displays.        |
|Type   | The listing type, which is only **Subscription** in this case.        |
|Installed   |The number of times the listing has been installed in your company's instance.        |
|Status   |The status of the subscription, which is either **Active**, **Canceled**, **Expiring on _Date_**, or **Payment required**.        |

To the right of each subscription in the list is an <img src="https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006uWCa" width="17"> action menu. When you select this menu, the following options appear:

| Menu option | Select this option to open |
| --- | --- |
| View listing | The listing Details page. |
| Manage listing | A menu with options to manage the subscription on Stripe or cancel the subscription. |
| View transactions | A page containing the transaction history for the subscription. |
| Cancel subscription | The same modal that displays when you [cancel a subscription](Manage-Subscriptions-to-Domo-Listings.html#cancel-a-subscription) from the listing Details page. |

## Cancel a subscription

{:  .important }
>There is no way to restore an app whose subscription has been canceled. Do not proceed unless you want to permanently remove an app from your company's instance.

1.  Select **Appstore** from the navigation header.
     

2.  Use the [search bar](ManageSubscriptionsDomoListings.html#subscribe-to-a-listing) on the **Search Apps** page to find and select the listing whose subscription you want to cancel.     
3.  On the listing Details page, select **Manage** \> **Cancel Subscription**.  
      
    ![Manage > Cancel Subscription](https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006ublN)  
      
    The **Cancel** _**Listing Name**_ **subscription** modal appears.  

      
    <img src="https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006ubob" width="470">
4.  Select the checkbox that reads "I understand that once this _Listing Name_ subscription is canceled _Number_ installation\[s\] will be deleted & removed permanently." This is required to enable the **Cancel Subscription** button.  
      
    <img src="https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006ublS" width="470">
5.  (Optional) Provide details about why you are canceling the subscription in the **Reason for cancelation** field.  
6.  In the last field, enter the word **CONFIRM** in all capital letters. This is required to enable the **Cancel Subscription** button.  
    
    <img src="https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006ublh" width="470">
7.  Select **Cancel Subscription**.   

    <img src="https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006ublr" width="470">

You are no longer subscribed to the listing, but you still have access to it until the next scheduled payment date, which displays in red text on the listing Details page. Renew the subscription before this date by following the steps to [renew a subscription](ManageSubscriptionsDomoListings#renew-a-subscription).  
  
![Next scheduled payment date](https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006ubmk)

## Renew a subscription

{:  .note }
>You can only renew a subscription within 30 days of cancellation.

1.  Select **Appstore** from the navigation header.
     

2.  Use the [search bar](Manage-Subscriptions-to-Domo-Listings.html#subscribe-to-a-listing) on the **Search Apps** page to find and select the listing whose subscription you want to cancel.  
3.  On the listing Details page, select **Manage Subscription**.  

    ![Manage Subscription](https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006ubmf)  

    You are redirected to Stripe, which displays your current and past subscriptions to the listing's publisher.  
4.  Select **Renew plan** for the subscription you want to renew. Canceled subscriptions have a **Canceled** tag above their name. 
       
    {:  .note }
    >To update your payment method, select <img src="https://github.com/haileytapia/portfolio/assets/78626762/deb886ce-d1d3-480b-9a17-91e76e38944f" width="26"> **Edit** before renewing the subscription.  
      
    ![Edit](https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006ubnJ)  

    The **Renew your plan** page opens.  
5.  Review the name, price, and renewal date of your plan, then select **Renew plan** to proceed with the renewal or **Go back** to exit.
      
    <img src="https://domo-support.domo.com/servlet/rtaImage?eid=ka05w00000128Er&feoid=00N5w00000Ri7BU&refid=0EM5w000006ubnT" width="300">

If the renewal is successful, you return to the previous page showing your current subscriptions; your subscription no longer has the **Canceled** tag above it.

In Domo, the subscription status changes from **Expiring on** _**Date**_ to **Active** in the **Installed Apps** > **Appstore Purchases** section. For more details about your subscription, see the [View your subscriptions](ManageSubscriptionsDomoListings#view-your-subscriptions) section of this article.

---

[Back to top](#top)

Thanks for visiting my portfolio! Don't hesitate to get in touch if you have any questions or feedback.
