---
title: "Dataset tools in Visual Studio"
ms.custom: na
ms.date: "10/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: "article"
f1_keywords: 
  - "vs.data.DataSet"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "aspx"
helpviewer_keywords: 
  - "untyped datasets"
  - "datasets [Visual Basic], extended properties"
  - "typed datasets"
  - "current record in dataset"
  - "XML [Visual Basic], datasets"
  - "DataSet class, about datasets"
  - "unique constraints (datasets)"
  - "data relationships"
  - "parent records in datasets"
  - "extended properties, in typed datasets"
  - "datasets [Visual Basic]"
  - "schemas [Visual Basic], datasets"
  - "datasets [Visual Basic], msprop"
  - "master-detail tables, datasets"
  - "databases [Visual Basic], updating"
  - "msprop"
  - "foreign keys, datasets"
  - "DataSet class"
  - "datasets [Visual Basic], filling"
  - "case sensitivity, datasets"
  - "constraints [Visual Basic], datasets"
  - "child records"
  - "related tables, datasets"
  - "updating datasets, about dataset updates"
  - "data caching, datasets"
  - "DataRelation object, datasets"
  - "untyped datasets, compared to typed datasets"
  - "cache [Visual Studio], datasets"
  - "datasets [Visual Basic], relationships"
  - "related tables"
  - "XML schemas, about XML schemas and datasets"
  - "relationships, datasets"
  - "typed datasets, compared to untyped datasets"
  - "datasets [Visual Basic], populating"
  - "datasets [Visual Basic], namespace"
  - "data adapters, populating datasets"
ms.assetid: ee57f4f6-9fe1-4e0a-be9a-955c486ff427
caps.latest.revision: 49
ms.author: "mblome"
manager: "ghogen"
translation.priority.ht: 
  - "de-de"
  - "es-es"
  - "fr-fr"
  - "it-it"
  - "ja-jp"
  - "ko-kr"
  - "ru-ru"
  - "zh-cn"
  - "zh-tw"
translation.priority.mt: 
  - "cs-cz"
  - "pl-pl"
  - "pt-br"
  - "tr-tr"
---
# Dataset tools in Visual Studio
> [!NOTE]
>  Datasets and related classes are legacy .NET technologies from the early 2000s that enable applications to work with data in memory while the applications are disconnected from the database. They are especially useful for applications that enable users to modify data and persist the changes back to the database. Although datasets have proven to be a very successful technology, we recommend that new .NET applications use Entity Framework. Entity Framework provides a more natural way to work with tabular data as object models, and it has a simpler programming interface.  
  
 A DataSet object is an in-memory object that is essentially a mini-database. It contains DataTable, DataColumn, and DataRow objects in which you can store and modify data from one or more databases without having to maintain an open connection. The dataset maintains information about changes to its data, so updates can be tracked and sent back to the database when your application becomes reconnected.  
  
 Datasets and related classes are defined in the System.Data namespace in the .NET Framework class library. You can create and modify datasets dynamically in code. For more information about how to do that, see ADO.NET. The documentation in this section shows how to work with datasets by using Visual Studio designers. One thing to know: datasets that are made through designers use TableAdapter objects to interact with the database, whereas datasets that are made programmatically use DataAdapter objects. For information about creating datasets programmatically, see [DataAdapters and DataReaders](../Topic/DataAdapters%20and%20DataReaders.md).  
  
 If your application needs to only read data from a database, and not perform updates, adds, or deletes, you can usually get better performance by using a DataReader object to retrieve data into a generic List object or another collection object. If you are displaying the data, you can data-bind the user interface to the collection.  
  
## Dataset workflow  
 Visual Studio provides a lot of tooling to simplify working with datasets. The basic end-to-end workflow is:  
  
-   Use the **Data Source** window to create a new dataset from one or more data sources. Use the **Dataset Designer** to configure the dataset and set its properties. For example, you need to specify which tables from the data source to include, and which columns from each table. Choose carefully to conserve the amount of memory that the dataset will require. For more information, see [Create and configure datasets](../datatools/create-and-configure-datasets-in-visual-studio.md).  
  
-   Specify the relationships between the tables so that foreign keys are handled correctly. For more information, see [Fill datasets by using TableAdapters](../datatools/fill-datasets-by-using-tableadapters.md).  
  
-   Use the **TableAdapter Configuration Wizard** to specify the query or stored procedure that will populate the dataset, and what database operations (update, delete, and so on) to implement. For more information, see these topics:  
  
    -   [Fill datasets by using TableAdapters](../datatools/fill-datasets-by-using-tableadapters.md)  
  
    -   [Edit data in datasets](../datatools/edit-data-in-datasets.md)  
  
    -   [Validate data in datasets](../datatools/validate-data-in-datasets.md)  
  
    -   [Save data back to the database](../datatools/save-data-back-to-the-database.md)  
  
-   Query and search the data in the dataset. For more information, see [Query datasets](../datatools/query-datasets.md). [!INCLUDE[linq_dataset](../datatools/includes/linq_dataset_md.md)] enables [LINQ (Language-Integrated Query)](../Topic/LINQ%20\(Language-Integrated%20Query\).md) over data in a \<xref:System.Data.DataSet> object. For more information, see [LINQ to DataSet](../Topic/LINQ%20to%20DataSet.md).  
  
-   Use the **Data Sources** window to bind user-interface controls to the dataset or its individual columns, and to specify which columns are user-editable. For more information, see [Bind controls to data in Visual Studio](../datatools/bind-controls-to-data-in-visual-studio.md).  
  
## Datasets and N-tier architecture  
 For information about datasets in N-tier applications, see [Work with datasets in n-tier applications](../datatools/work-with-datasets-in-n-tier-applications.md).  
  
## Datasets and XML  
 For information about converting datasets to and from XML, see [Read XML data into a dataset](../datatools/read-xml-data-into-a-dataset.md) and [Save a dataset as XML](../datatools/save-a-dataset-as-xml.md).  
  
## See Also  
 [Visual Studio data tools for .NET](../datatools/visual-studio-data-tools-for-.net.md)