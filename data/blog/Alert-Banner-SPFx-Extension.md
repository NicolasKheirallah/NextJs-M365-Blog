---
date: '2024-10-11T01:49:22.412Z'
title: Alert Banner for SharePoint online
description: I have developed a dynamic alert banner, a customizable notification component prominently displayed in the header of Modern SharePoint sites. It is designed to effectively communicate important information, updates, or announcements to users in a clear and concise manner.
tags: ['SharePoint', 'Graph', 'SPFX']
summary: I created a customizable notification component in SharePoint headers designed to effectively communicate important updates and information to users.
authors: ['default']
---

# Introducing the Alert Banner SPFx Extension: Elevate Your SharePoint Experience with Dynamic Alerts

![Alert Banner Screenshot](https://github.com/NicolasKheirallah/AlertBanner/blob/main/Screenshot/Screenshot2024-08-17170932.png)

In today's fast-paced business environment, I understand how crucial effective communication is. SharePoint, being a cornerstone of Microsoft 365, offers a robust platform for collaboration and information sharing. However, I've noticed that organizations often seek enhanced ways to deliver critical updates and notifications directly within their SharePoint sites. This realization led me to develop the **Alert Banner SPFx Extension**—a custom SharePoint Framework (SPFx) extension designed to display dynamic alert notifications in the header of Modern SharePoint sites.

## What is the Alert Banner SPFx Extension?

The **Alert Banner SPFx Extension** is my tailored solution that integrates seamlessly with SharePoint's Modern UI to provide real-time alert notifications. These alerts are fetched from a designated SharePoint list using the Microsoft Graph API, ensuring that users receive timely and relevant information without navigating away from their current page.

![SharePoint Alert Banner](https://github.com/NicolasKheirallah/AlertBanner/blob/main/Screenshot/Screenshot2024-08-17170932.png)

## Key Features

### **Dynamic Alert Retrieval**

I've leveraged the Microsoft Graph API to fetch alerts from a specific SharePoint list. This dynamic retrieval ensures that alerts are always up-to-date and managed centrally, eliminating the need for manual updates or code modifications.

### **Prominent Banner Display**

Alerts are displayed prominently in the header of Modern SharePoint pages, ensuring high visibility. This strategic placement guarantees that important messages catch users' attention immediately upon accessing the site.

### **Customizable Alert Types**

Administrators can define various alert types—such as Info, Warning, Maintenance, and Interruption—each with its own unique styling and iconography. This customization allows for clear differentiation between different types of alerts, enhancing user comprehension and response.

### **User Interaction Handling**

Users have the ability to dismiss alerts, with the system remembering their preferences using session storage. This feature ensures a non-intrusive experience, preventing dismissed alerts from reappearing unnecessarily during the same session.

### **Performance Optimization**

By utilizing local storage for caching alerts, the extension minimizes redundant data fetching, leading to improved performance and faster load times, even in environments with limited network bandwidth.

## Benefits of Using the Alert Banner SPFx Extension

- **Enhanced Communication:** Deliver critical updates directly within the SharePoint interface, ensuring that users are always informed.
- **Centralized Management:** Manage all alerts from a single SharePoint list, streamlining the process of creating, updating, and deleting alerts.
- **Flexibility and Customization:** Tailor alert types to match organizational needs and branding, providing a cohesive and professional appearance.
- **Improved User Experience:** Non-intrusive alert display and user-friendly interactions promote a seamless and efficient user experience.

## How to Get Started

### **Prerequisites**

Before deploying the Alert Banner SPFx Extension, ensure you have the following:

- **Node.js** (v18.x or later)
- **React 17**
- **SPFx** (v1.19.x or later)
- A **SharePoint Online** site collection
- Appropriate permissions to access and configure the tenant App Catalog

### **Installation Steps**

1. **Clone the Repository**
   Begin by cloning the repository to your local machine:
   ```bash
   git clone https://github.com/NicolasKheirallah/AlertBanner.git
   ```

````

2. **Navigate to the Solution Folder**

   ```bash
   cd AlertBanner
   ```

3. **Install Dependencies**
   Install the necessary packages using npm:

   ```bash
   npm install
   ```

4. **Build the Project**
   Compile the project to ensure all components are correctly set up:

   ```bash
   gulp build  && gulp bundle --ship && gulp package-solution --ship
   ```

5. **Deploy to App Catalog**
   - Package the solution.
   - Upload it to your SharePoint tenant's App Catalog.
   - Approve any necessary permissions.
   - Deploy the extension to your desired site collections.
````

## Managing Alerts

### **Global Alerts**

Once deployed, the extension fetches alerts from the root site, ensuring consistency across all sites within your tenant. This centralized approach simplifies the management of alerts, making it easier to broadcast important messages universally.

### **Local Alerts**

For site-specific alerts, a new list titled "Alerts" is automatically created in the Site Contents of each site collection where the extension is deployed. Administrators can add new alerts by simply adding items to this list.

#### **Alert List Configuration:**

- **Title:** The main heading of the alert.
- **Description:** Detailed message content.
- **AlertType:** Defines the type of alert (e.g., Info, Warning, Maintenance, Interruption).
- **Link:** Optional URL for additional information or related content.

### **Dynamic Alert Type Configuration**

Administrators can customize alert types using a JSON configuration property. This flexibility allows for easy addition, modification, or removal of alert types without altering the underlying codebase.

**Example JSON Structure:**

```json
{
  "Info": {
    "iconName": "Info12",
    "backgroundColor": "#389899",
    "textColor": "#ffffff",
    "additionalStyles": ""
  },
  "Warning": {
    "iconName": "ShieldAlert",
    "backgroundColor": "#f1c40f",
    "textColor": "#ffffff",
    "additionalStyles": ""
  },
  "Maintenance": {
    "iconName": "CRMServices",
    "backgroundColor": "#afd6d6",
    "textColor": "#ffffff",
    "additionalStyles": ""
  },
  "Interruption": {
    "iconName": "IncidentTriangle",
    "backgroundColor": "#c54644",
    "textColor": "#ffffff",
    "additionalStyles": ""
  }
}
```

> **Tip:** Store this JSON in your tenant-wide extension component properties to enable centralized management and easy updates.

## Future Enhancements

While the Alert Banner SPFx Extension already offers robust functionality, there are plans to further enhance its capabilities:

- **Enhanced Design:** Improve the visual aesthetics and provide more CSS customization options to match diverse organizational branding.
- **Advanced Sorting:** Implement sorting mechanisms for alerts based on priority levels and dates to ensure the most critical alerts are displayed first.

## Community and Contributions

This project is open-source and welcomes contributions from the community. Whether you're looking to suggest new features, report bugs, or contribute code, your involvement is invaluable in making the Alert Banner SPFx Extension even better.

## References

- [Getting Started with SharePoint Framework](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/set-up-your-developer-tenant)
- [Building for Microsoft Teams](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/build-for-teams-overview)
- [Use Microsoft Graph in Your Solution](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/get-started/using-microsoft-graph-apis)
- [Publish SharePoint Framework Applications to the Marketplace](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/publish-to-marketplace-overview)
- [Microsoft 365 Patterns and Practices](https://aka.ms/m365pnp) - Guidance, tooling, samples, and open-source controls for your Microsoft 365 development.

## Concepts Demonstrated

The Alert Banner SPFx Extension showcases several advanced concepts and best practices within the SharePoint and SPFx ecosystems:

- **Integration of the Microsoft Graph API:** Efficiently retrieves data from SharePoint lists, enabling dynamic content updates.
- **Dynamic Configuration Management:** Utilizes JSON properties to define alert types, enhancing flexibility and maintainability.
- **Customizing Modern SharePoint Banners:** Leverages SPFx extensions to modify and enhance the user interface of SharePoint sites.
- **State Management and Caching:** Implements local and session storage to optimize performance and ensure a smooth user experience.
- **Responsive and Accessible Design:** Ensures that alerts are displayed effectively across various devices and adhere to accessibility standards.

## Conclusion

The **Alert Banner SPFx Extension** fills a critical gap by providing organizations with a customizable and efficient way to communicate important information directly within their SharePoint environments. By leveraging the power of the Microsoft Graph API and embracing best practices in SPFx development, this extension offers a seamless and scalable solution for modern collaboration needs.

Whether you're an IT administrator seeking to improve internal communications or a developer looking to contribute to the SharePoint community, the Alert Banner SPFx Extension is a valuable tool that enhances the functionality and usability of your SharePoint sites.

> **Get Started Today:** Clone the repository, customize your alert types, and deploy the extension to transform how your organization communicates within SharePoint.

For more information, updates, and to contribute to the project, visit the [Alert Banner GitHub Repository](https://github.com/NicolasKheirallah/AlertBanner).

---

**Disclaimer:** _THIS CODE IS PROVIDED *AS IS* WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING ANY IMPLIED WARRANTIES OF FITNESS FOR A PARTICULAR PURPOSE, MERCHANTABILITY, OR NON-INFRINGEMENT._

```

```

```

```
