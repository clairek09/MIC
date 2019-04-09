
Once the workspace is created, you can start to build and train models.  (updated by Star 2019/04/09 20:01)

Training a machine learning model could be as easy as loading the data and running one line of code from packages like Scikit-Learn, but most of the time the process requires more. Before you apply different models, you need to understand how the dataset looks and apply the best model.

In this module, you will use the MNIST dataset as an example to explore the Azure Machine Learning service. You can build and train your model both locally or via remote containers. You  train a simple logistic regression model and a series of kNN models to find the one with the highest accuracy. This example is an image classification problem in which you want to determine the number contained in an image.

## Learning Objectives

In this module you will:

- Create a simple logistic model to recognize numbers contained in images from the MNIST dataset
- Create a series of kNN models to find the one with the highest accuracy
- Create an Azure Machine Learning experiment
- Train a model using the Azure Machine Learning service
- Submit the model, monitor the run, and retrieve the results


### What is the Internet?

**The Internet** connects people across the world to one another, through a massive global network of computers and devices. With the Internet you can communicate with people across the world, access and share information.

**Watch the following video to learn more about the Internet and what it means to connect to the Internet.**


#### Video: What is the Internet?
> [!VIDEO https://www.youtube.com/embed/QaCa5U6gr0E]

### Connect to the Internet

To access information and communicate with others using the Internet, you'll first need to connect to the Internet- or "go online". There are several ways to connect to the Internet, including both wireless and wired connections.

**Watch the following video to learn how to connect to the Internet.**


#### Video: Connect to the Internet
> [!VIDEO https://www.youtube.com/embed/JF7XqrrMzl4]

### Connect to a Wireless Network

You may often need to connect a portable device to the Internet when you're on-the-go or in a temporary location.  You can connect to the Internet wirelessly using Wi-Fi.

**Watch the following video to learn how to connect a Windows 10 device to a network using Wi-Fi.**


#### Video: Connect to a wireless network
> [!VIDEO https://www.youtube.com/embed/SDJlqWYFU0s]


### Try It Yourself

Check the Wi-Fi connection status of your computer.  Are you connected to a network?  Are there any networks that you have access to join?

quiz:
  title: Check your knowledge
  questions:

  - content: "Virtual hard drive files (VHDs) are stored in which of the following types of blobs in Azure Storage?"
    choices: 
    - content: "Block Blobs"
      isCorrect: false
      explanation: "VHDs are backed by page blobs in Azure Storage. Page blobs are appropriate because they are a collection of 512-byte pages optimized for random read and write. Neither Block blobs nor Append blobs are optimized for the random read and write operations common with VHDs."
    - content: "Append Blobs"
      isCorrect: false
      explanation: "VHDs are backed by page blobs in Azure Storage. Page blobs are appropriate because they are a collection of 512-byte pages optimized for random read and write. Neither Block blobs nor Append blobs are optimized for the random read and write operations common with VHDs."
    - content: "Page Blobs"
      isCorrect: true
      explanation: "VHDs are backed by page blobs in Azure Storage. Page blobs are appropriate because they are a collection of 512-byte pages optimized for random read and write. Neither Block blobs nor Append blobs are optimized for the random read and write operations common with VHDs."

  - content: "Which of the following data-replication strategies is the only option supported by a premium storage account?"
    choices: 
    - content: "Read-access geo-redundant storage (RA-GRS)"
      isCorrect: false
      explanation: "A premium storage account supports only locally redundant storage as the replication option. Locally redundant storage keeps three copies of the data within a single region. For regional disaster recovery, you must back up your VM disks in a different region by using Azure Backup. You also must use a geo-redundant storage (GRS) account as the backup vault."
    - content: "Locally redundant storage (LRS)"
      isCorrect: true
      explanation: "A premium storage account supports only locally redundant storage as the replication option. Locally redundant storage keeps three copies of the data within a single region. For regional disaster recovery, you must back up your VM disks in a different region by using Azure Backup. You also must use a geo-redundant storage (GRS) account as the backup vault."
    - content: "Geo-redundant storage (GRS)"
      isCorrect: false
      explanation: "A premium storage account supports only locally redundant storage as the replication option. Locally redundant storage keeps three copies of the data within a single region. For regional disaster recovery, you must back up your VM disks in a different region by using Azure Backup. You also must use a geo-redundant storage (GRS) account as the backup vault."
    - content: "Zone-redundant storage (ZRS)"
      isCorrect: false
      explanation: "A premium storage account supports only locally redundant storage as the replication option. Locally redundant storage keeps three copies of the data within a single region. For regional disaster recovery, you must back up your VM disks in a different region by using Azure Backup. You also must use a geo-redundant storage (GRS) account as the backup vault."

  - content: "Which of the following disk types is only available for managed disks?"
    choices: 
    - content: "Standard solid-state drives (SSDs)"
      isCorrect: true
      explanation: "Choosing managed disks gives you the option of using standard SSDs. This disk type is between standard HDDs and premium SSDs from a performance and cost perspective."
    - content: "Standard hard disk drives (HDDs)"
      isCorrect: false
      explanation: "Choosing managed disks gives you the option of using standard SSDs. This disk type is between standard HDDs and premium SSDs from a performance and cost perspective."
    - content: "Premium solid-state drives (SSDs)"
      isCorrect: false
      explanation: "Choosing managed disks gives you the option of using standard SSDs. This disk type is between standard HDDs and premium SSDs from a performance and cost perspective."