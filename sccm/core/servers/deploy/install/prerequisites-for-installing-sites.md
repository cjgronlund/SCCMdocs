---
title: "Prerequisites for sites | Microsoft Docs"
description: "Learn about prerequisites for installing the different types of System Center Configuration Manager sites."
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# Prerequisites for installing System Center Configuration Manager sites

*Applies to: System Center Configuration Manager (Current Branch)*

Before you begin a site installation, it's a good idea to learn about the prerequisites for installing the different types of System Center Configuration Manager sites.

## Primary sites and the central administration site
The following prerequisites apply to installing a central administration site as the first site of a hierarchy, installing a stand-alone primary site, or installing a child primary site. If you are installing a central administration site as part of a hierarchy expansion, see [Expanding a stand-alone primary site](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand) in this topic.

###  <a name="bkmk_PrereqPri"></a> Prerequisites for installing a primary site or a central administration site  

-   The user account that installs the site must have the following rights:  

    -   **Administrator** on the site server computer  
    -   **Administrator** on each computer that will host the **site database** or an instance of the **SMS Provider** for the site  
    -   **Sysadmin** on the instance of SQL Server that hosts the site database  

        > [!IMPORTANT]  
        >  When Setup finishes, both the user account that runs Setup and the site server computer account must retain sysadmin rights to SQL Server. Do not remove the sysadmin rights from these accounts.  

-   If you are installing a primary site, you need the following additional rights:  
    -  **Administrator** on additional computers where you will install the initial management point and distribution point, if not on the site server  

-   If you are installing a new child primary site below a central administration site, you need the following additional rights:  

    -   **Administrator** on the computer that hosts the central administration site  

    -   Role-based administration rights within Configuration Manager that are equivalent to the security role of **Infrastructure Administrator** or **Full Administrator**  

-   You must use the correct installation media (source files), and run Setup from that location. For information about the correct source files to use to install different types of sites, see [Options for installing different types of sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) in the [Prepare to install sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md) topic.

-   The site server computer must have access to updated Setup files from Microsoft, in one of these ways:
    -  Before you start the install, you can download and store a copy of these files on your local network by using [Setup Downloader](../../../../core/servers/deploy/install/setup-downloader.md).
    -  If a local copy of these file is not available, the site server must have Internet access so it can download these files from Microsoft during the installation.

- Before you can expand a stand-alone primary site that has a service connection point site system role installed, you must uninstall the service connection point. Only one instance of this role is permitted in a hierarchy, and it is only permitted at the top-tier site of the hierarchy. You will have the opportunity to reinstall the role during the installation of the central administration site.
- The site server and site database computers must meet all prerequisite configurations. Before starting Setup, you can [manually run Prerequisite Checker](../../../../core/servers/deploy/install/prerequisite-checker.md) to identify and fix problems.  


### <a name="bkmk_expand"></a> Expanding a stand-alone primary site
A stand-alone primary site must meet the following prerequisites before you can expand it into a hierarchy with a central administration site:

-   **You must install the new central administration site installation media (which contains the source files) that matches the version of the stand-alone primary site**

     To ensure a version match, install the new site by using the source files found in the [CD.Latest folder](../../../../core/servers/manage/the-cd.latest-folder.md) on the stand-alone primary site.

     For more information about the correct source files to use to install different sites, see [Options for installing different types of sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) in the [Prepare to install sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md) topic.


-   **The stand-alone primary site cannot be configured to migrate data from another Configuration Manager hierarchy**  

     You must stop active migration to the stand-alone primary site from other Configuration Manager hierarchies and remove all configurations for migration. This includes migration jobs that have not completed, data gathering, and the configuration of the active source hierarchy.  

     This is necessary because migration operations are performed by the top-tier site of the hierarchy, and the configurations for migration do not transfer to the central administration site when you expand a stand-alone primary site.  

     After you expand the stand-alone primary site, if you reconfigure migration at the primary site, the central administration site performs the migration-related operations. For more information about how to configure migration, see [Configure source hierarchies and source sites for migration to System Center Configuration Manager](../../../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

-   **The computer account of the computer that will host the new central administration site must be a member of the Administrator user group on the standa-lone primary site**  

     To successfully expand the stand-alone primary site, the computer account of the new central administration site must have **Administrator** rights on the stand-alone primary site. This is required only during site expansion. The account can be removed from the user group on the primary site when site expansion is finished.  

-   **The user account that runs Setup to install the new central administration site must have role-based administration rights at the stand-alone primary site**  

     To install a central administration site as part of a site expansion, the user account that runs Setup to install the central administration site must be defined in role-based administration at the stand-alone primary site as either a **Full Administrator** or an **Infrastructure Administrator**.  

-   **You must uninstall the following site system roles from the stand-alone primary site before you can expand the site:**  

    -   Asset Intelligence sync point  
    -   Endpoint Protection point  
    -   Service connection point  

   These site system roles are supported only at the top-tier site of the hierarchy. Therefore, you must uninstall these site system roles before you expand the stand-alone primary site. After you expand the site, you can reinstall these site system roles at the central administration site.  

    All other site system roles can remain installed at the primary site.  

-   **The port for the SQL Server Service Broker (SSB) between the stand-alone primary site and the computer that will install the central administration site must be open**  

     To successfully replicate data between a central administration site and a primary site, Configuration Manager requires an open port between the two sites for SSB to use. When you install a central administration site and expand a stand-alone primary site, the prerequisite check does not verify that the port you specify for the SSB is open on the primary site.  


## <a name="bkmk_secondary"></a> Secondary sites
The following are prerequisites for installing secondary sites:
-   The administrator who configures the installation of the secondary site in the Configuration Manager console must have role-based administration rights that are equivalent to the security role of **Infrastructure Administrator** or **Full Administrator**.  
-   The computer account of the parent primary site must be an **Administrator** on the secondary site server computer.  
-   When the secondary site uses a previously installed instance of SQL Server to host the secondary site database:  

    -   The **computer account** of the parent primary site must have **sysadmin** rights on the instance of SQL Server on the secondary site server computer.  

    -   The **Local System** account of the secondary site server computer must have **sysadmin** rights on the instance of SQL Server on the secondary site server computer.  

        > [!IMPORTANT]  
        >  When Setup finishes, both accounts must retain sysadmin rights to SQL Server. Do not remove the sysadmin rights from these accounts.  

-   The secondary site server computer must meet all prerequisite configurations, which includes SQL Server and the default site system roles of the management point and distribution point.  
