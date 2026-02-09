# **Azure AI Services**

Think of AI as software that exhibits one or more human-like capabilities.
1. **Visual perception** - The ability to use computer vision capabilities to accept, interpret, and process input from images, video streams, and live cameras.
2. **Text analysis and conversation** - The ability to use natural language processing (NLP) to not only "read", but also generate realistic responses and extract semantic meaning from text.
3. **Speech** - The ability to recognize speech as input and synthesize spoken output. The combination of speech capabilities together with the ability to apply NLP analysis of text enables a form of human-compute interaction that's become known as conversational AI.
4. **Decision making** - The ability to use past experience and learned correlations to assess situations and take appropriate actions. For example, recognizing anomalies in sensor readings and taking automated action to prevent failure or system damage.

**AI-related terms**
1. **Data science**: Data science is an interdisciplinary field that focuses on the processing and analysis of data; applying statistical techniques to uncover and visualize relationships and patterns in the data, and defining experimental models that help explore those patterns. Data scientist might gather samples of data about the population of an endangered species in a geographical area, and combine it with data about levels of industrialization and economic demographics in the same area.
2. **Machine learning**: Data scientists often work with machine learning models. Machine learning deals with the training and validation of predictive models. Typically, a data scientist prepares the data and then uses it to train a model based on an algorithm that exploits the relationships between the features in the data to predict values for unknown labels. **Use factors**: such as the number of nesting sites observed, the area of land designated as protected, the human population in the local area, the daily volume of traffic on local roads, and so on. **evaluate plan**: for housing, infrastructure, and industrial development in the local area and assess their likely impact on the local wildlife
3. **Artificial intelligence**: Artificial intelligence (AI) describes software that emulates one or more characteristics of human intelligence. Machine learning is a prominent approach used to create AI software. Knowledge of data science can support an understanding of artificial intelligence. **a predictive model** could be trained to analyze image data taken by motion-activated cameras in remote locations, and predict whether a photograph contains a sighting of the animal

* After the model has been trained, you can submit new data that includes known feature values and have the model predict the most likely label. Using the model to make predictions is referred to as **inferencing**.
* Software developers should make use of **confidence score** values to evaluate predictions and apply appropriate thresholds to optimize application reliability and mitigate the risk of predictions that may be made based on marginal probabilities.
* software engineers building AI-enabled solutions should apply due consideration to **mitigate risks and ensure fairness, reliability, and adequate protection from harm or discrimination.**
* Responsible AI: Fairness, Reliability and safety, Privacy and Security, Inclusiveness, Transparency, Accountability.
* **Automated machine learning**: This feature enables **non-experts to quickly create an effective machine learning model** from data.
* **Azure Machine Learning designer**:	A graphical interface enabling **no-code development** of machine learning solutions.
* **Data and compute management**: **Cloud-based data storage and compute resources** that professional data scientists can use to run data experiment code at scale.
* **Pipelines**:	Data scientists, software engineers, and IT operations professionals can define pipelines to **orchestrate model training, deployment, and management tasks**.

Software engineers may interact with Azure Machine Learning in the following ways:
1. Using Automated Machine Learning or Azure Machine Learning designer to train machine learning models and deploy them as services that can be integrated into AI-enabled applications.
2. Collaborating with data scientists to deploy models based on common frameworks such as Scikit-Learn, PyTorch, and TensorFlow as web services, and consume them in applications.
3. **Using Azure Machine Learning SDKs or command-line interface (CLI) scripts** to orchestrate DevOps processes that manage versioning, deployment, and testing of machine learning models as part of an overall application **delivery solution**.

![image](https://github.com/user-attachments/assets/1051515f-9d20-487f-9a61-2c7166480826)

* Azure OpenAI Service is an Azure AI service for deploying, utilizing, and fine-tuning models developed by OpenAI. AI engineers can develop applications that use the powerful generative AI models in Azure OpenAI to further utilize this technology. Both REST and language specific SDKs are available when developing applications.
* In addition to basic text-based indexing, Azure AI Search enables you to define an **enrichment pipeline** that uses AI skills to enhance the index with insights derived from the source data - for example, by using computer vision and natural language processing capabilities to generate descriptions of images, extract text from scanned documents, and determine key phrases in large documents that encapsulate their key points.
* Not only does this AI enrichment produce a more useful search experience, **the insights extracted by your enrichment pipeline can be persisted in a knowledge store for further analysis or integration into a data pipeline for a business intelligence solution**.

To consume the service through the endpoint, applications require the following information:
1. **The endpoint URI**. This is the HTTP address at which the REST interface for the service can be accessed.
2. **A subscription key**. Client applications must provide a valid key to consume the service. When you provision an AI services resource, two keys are created - applications can use either key.
3. **The resource location**. When you provision a resource in Azure, you generally assign it to a location, which determines the Azure data center in which the resource is defined. While most SDKs use the endpoint URI to connect to the service, some require the location.

### Secure Azure AI services
You can regenerate **subscription keys** using the Azure portal, or using the az cognitiveservices account keys regenerate Azure command-line interface (CLI) command.

* **Token-based authentication**
  When using the REST interface, some AI services support (or even require) token-based authentication. In these cases, the subscription key is presented in an initial request to obtain an authentication token, which has a valid period of 10 minutes. Subsequent requests must present the token to validate that the caller has been authenticated. When using an SDK, the calls to obtain and present a token are handled for you by the SDK.
* **Microsoft Entra ID authentication**
Azure AI services supports Microsoft Entra ID authentication, enabling you to grant access to specific service principals or managed identities for apps and services running in Azure.
* **Authenticate using service principals**
  1. Create a custom subdomain
  2. Assign a role to a service principal
  3. Authenticate using managed identities

`az ad sp create-for-rbac -n "api://ai-app-ta0011" --role owner --scopes subscriptions/9937e55a-6e56-470d-83d7-a31e3f5e27bb/resourceGroups/rg-01
{
    "appId": "abcd12345efghi67890jklmn",
    "displayName": "api://ai-app-",
    "password": "1a2b3c4d5e6f7g8h9i0j",
    "tenant": "1234abcd5678fghi90jklm"
}

az ad sp show --id <appId-use-from-above>

az keyvault set-policy -n <keyVaultName> --object-id <objectId-use-from-above> --secret-permissions get list`

**Apply network access restrictions**
By default, Azure AI services are accessible from all networks. Some individual AI services resources (such as Azure AI Face service, Azure AI Vision, and others) can be configured to restrict access to specific network addresses - either public Internet addresses or addresses on virtual networks.

### Monitor Azure AI services
To create an alert rule for an Azure AI services resource, select the resource in the Azure portal and on the Alerts tab, add a new alert rule. To define the alert rule, you must specify:

* The scope of the alert rule - in other words, the resource you want to monitor.
* A condition on which the alert is triggered. The specific trigger for the alert is based on a signal type, which can be Activity Log (an entry in the activity log created by an action performed on the resource, such as regenerating its subscription keys) or Metric (a metric threshold such as the number of errors exceeding 10 in an hour).
* Optional actions, such as sending an email to an administrator notifying them of the alert, or running an Azure Logic App to address the issue automatically.
* Alert rule details, such as a name for the alert rule and the resource group in which it should be defined.

In the case of Azure AI services, Azure Monitor collects metrics relating to endpoint requests, data submitted and returned, errors, and other useful measurements.
Diagnostic logging enables you to capture rich operational data for an Azure AI services resource, which can be used to analyze service usage and troubleshoot problems. **Diagnostic settings enable you to capture data for subsequent analysis**.

To capture diagnostic logs for an AI services resource, you need a destination for the log data. You can use Azure Event Hubs as a destination in order to then forward the data on to a custom telemetry solution, and you can connect directly to some third-party solutions; but in most cases you'll use one (or both) of the following kinds of resource within your Azure subscription:

Azure Log Analytics - a service that enables you to query and visualize log data within the Azure portal.
Azure Storage - a cloud-based data store that you can use to store log archives (which can be exported for analysis in other tools as needed). create the Azure Storage account in the same region as your AI services resource.

### Deploy Azure AI services in containers

Language containers, Speech containers, Vision containers
Azure AI services container images example. Complete list can be found at: https://learn.microsoft.com/en-us/training/modules/investigate-container-for-use-with-ai-services/3-use-ai-services-container

mcr.microsoft.com/azure-cognitive-services/textanalytics/keyphrase
mcr.microsoft.com/**product**/azure-cognitive-services/textanalytics/language/**about**

You can use the Docker pull command to download container images to work with them directly from your machine. Some of the containers are in a "Gated" public preview state, and you need to explicitly request access to use them. Otherwise the containers are available for anyone to use with their Azure AI services deployment.

When you deploy an Azure AI services container image to a host, you must specify three settings.
ApiKey: Key from your deployed Azure AI service; used for billing.
Billing	Endpoint: URI from your deployed Azure AI service; used for billing.
Eula: Value of accept to state you accept the license for the container.

### Azure AI Content Safety

#### Safeguarding text content
1. **Moderate text** scans text across four categories: **violence, hate speech, sexual content, and self-harm**. A **severity level from 0 to 6** is returned for each category. 
2. **Prompt shields** is a unified API to identify and block jailbreak attacks from inputs to LLMs.
3. **Protected material** detection checks AI-generated text for protected text such as recipes, copyrighted song lyrics, or other original material.
4. **Groundedness detection** protects against inaccurate responses in AI-generated text by LLMs. An ungrounded response is one where the model's output varies from the source information. Groundedness detection includes a reasoning option in the API response. This adds a reasoning field that explains any ungroundedness detection. **However, reasoning increases processing time and costs**.

#### Safeguarding image content
1. **Moderate images** scans for inappropriate content across four categories: violence, self-harm, sexual, and hate. **A severity level is returned: safe, low, or high**. You then set a **threshold level of low, medium, or high**. The combination of the severity and threshold level determines whether the image is allowed or blocked for each category.
2. **Moderate multimodal content** scans both images and text, including text extracted from an image using optical character recognition (OCR). Content is analyzed across four categories: violence, hate speech, sexual content, and self-harm.

#### Custom safety solutions
1. **Custom categories** enables you to create your own categories by providing positive and negative examples, and training the model. Content can then be scanned according to your own category definitions.
2. **Safety system message** helps you to **write effective prompts** to guide an AI system's behavior.

#### Evaluating accuracy
When evaluating how accurately Azure AI Content Safety is for your situation, compare its performance against four criteria:

* True positive - correct identification of harmful content.
* False positive - incorrect identification of harmful content.
* True negative - correct identification of harmless content.
* False negative - harmful content isn't identified.

-----
# **Azure AI Vision**

![image](https://github.com/user-attachments/assets/54821354-7c6a-4aa6-8ae8-8403d4e4f6ba)

* smart-cropped thumbnail: You can specify the aspect ratio of the cropped image (width / height), ranging from 0.75 to 1.80.
* When creating an alpha matte of an image, the result is the foreground in all white, with a black background. Alpha matte images are helpful when client applications intend to do further processing of an image that requires separation of foreground and background objects.

* Image classification: Models can be trained for multi-class classification (where there are **multiple classes, but each image can belong to only one class**) or multi-label classification (where an **image might be associated with multiple labels**).
* Object detection:
  There are two components to object detection:
  * The **class label of each object** detected in the image. For example, you might predict that an image contains one apple and two oranges.
  * The **location of each object** within the image, indicated as coordinates of a bounding box that encloses the object.
* Product recognition: Product recognition works the same way object detection does, but with improved accuracy for product labels and brand names.

A COCO file is a JSON file with a specific format that defines:
* **images**: Defines the image location in blob storage, name, width, height, and ID.
* **annotations**: Defines the classifications (or objects), including which category the image is classified as, the area, and the bounding box (if labeling for object detection).
* **categories**: Defines the ID for the named label class.

area: integer	Value of 'Width' x 'Height' (third and fourth values of bbox)

bbox: list[float]	Relative coordinates of the bounding box (0 to 1), in the order of 'Left', 'Top', 'Width', 'Height'

* When training a model select the **model type**, specify the **dataset** you want to use as training data, and indicate the **training budget**. The training budget is an upper bound of time for how long the training will run; the actual time used for training is often less than the specified budget.
* You need about 3-5 images per class to train a custom image classification model with Azure AI Vision.
* To use the Azure AI Custom Vision service, you must provision two kinds of Azure resource: A training resource & A prediction resource.
* To train an image classification model with the Azure AI Custom Vision service, you can use the Azure AI Custom Vision portal, the Azure AI Custom Vision REST API or SDK, or a combination of both approaches. The REST API and SDKs enable you to perform the same tasks by writing code, which is useful if you need to automate model training and publishing as part of a DevOps process.
* While image classification requires **one or more tags** that apply to the whole image, object detection requires that each label consists of a **tag and a region** that defines the bounding box for each object in an image.
* after tagging an initial batch of images, you can train the model. Subsequent labeling of new images can benefit from the smart labeler tool in the portal, which can suggest not only the regions, but the classes of object they contain.
* Bounding box

  ![image](https://github.com/user-attachments/assets/2767350f-0f96-4f09-8298-c5372d3d1a6e)

#### The Face service

The Face service offers more comprehensive facial analysis capabilities than the Azure AI Vision service, including:

* Face detection (with bounding box).
* Comprehensive facial feature analysis (including head pose, presence of spectacles, blur, facial landmarks, occlusion and others).
* Face comparison and verification.
* Facial recognition.

* If you want to use the identification, recognition, and verification features of Face, you'll need to apply for the Limited Access policy and get approval before these features are available.
* When a face is detected by the Face service, a unique ID is assigned to it and retained in the service resource for 24 hours. The ID is a GUID, with no indication of the individual's identity other than their facial features.
* The trained model is stored in your Face (or Azure AI Services) resource, and can be used by client applications to (Person Group, Person and identified faces):
  1. Identify individuals in images.
  2. Verify the identity of a detected face.
  3. Analyze new images to find faces that are similar to a known, persisted face.

#### Azure AI Vision options for reading text

Azure AI Vision Service & Azure AI Document Intelligence. access via the REST API or a client library

* Image Analysis Optical character recognition (OCR):
  * Use this feature for general, **unstructured documents with smaller amount of text, or images that contain text**.
  * The Image Analysis service OCR feature is best suited for short sections of handwritten text.
  * Results are returned immediately (**synchronous**) from a single API call.
  * Has functionality for analyzing images past extracting text, including object detection, describing or categorizing an image, generating smart-cropped thumbnails and more.
  * Examples include: street signs, handwritten notes, and store signs.
  * Read API
    * Python:
      `
      result = client.analyze(
          image_url=<image_to_analyze>,
          visual_features=[VisualFeatures.READ]
      )
      `

    * REST API: `https://<endpoint>/computervision/imageanalysis:analyze?features=read&...`
    * Read OCR function are returned synchronously, either as JSON or the language specific object of a similar structure.
    * These results are broken down in **blocks, then lines, and then words**. Additionally, the text values are included at both the line and word levels, making it easier to read entire lines of text if you don't need to extract text at the individual word level. Results also contain bounding boxes for each word and line.
      
* Document Intelligence:
  * Use this service to read small to large volumes of text from images and PDF documents.
  * The Document Intelligence API can be used to process PDF formatted files.
  * This service uses **context and structure of the document to improve accuracy**.
  * The initial function call returns an **asynchronous** operation ID, which must be used in a subsequent call to retrieve the results.
  * Examples include: receipts, articles, and invoices.

#### Analyze video

* The Azure Video Indexer service is designed to help you extract information from videos. It provides functionality that you can use for:
1. Facial recognition - detecting the presence of individual people in the image. This requires Limited Access approval.
2. Optical character recognition - reading text in the video.
3. Speech transcription - creating a text transcript of spoken dialog in the video.
4. Topics - identification of key topics discussed in the video.
5. Sentiment - analysis of how positive or negative segments within the video are.
6. Labels - label tags that identify key objects or themes throughout the video.
7. Content moderation - detection of adult or violent themes in the video.
8. Scene segmentation - a breakdown of the video into its constituent scenes.

* You can extend the recognition capabilities of Video Analyzer by creating custom models for: People, Language & Brands.
* Brand detection identifies the mention of products, services, and companies suggested by Bing's brands database. For example, if Microsoft is mentioned in a video or audio content or if it shows up in visual text in a video, Azure AI Video Indexer detects it as a brand. You can both detect known brands, and well as include new brands you want to detect by providing information about it.
* Azure Video Indexer widgets: The widgets used in the Azure Video Indexer portal to play, analyze, and edit videos can be embedded in your own custom HTML interfaces. You can use this technique to share insights from specific videos with others without giving them full access to your account in the Azure Video Indexer portal.
* Azure Video Indexer API:
  * To get access token: `https://api.videoindexer.ai/Auth/<location>/Accounts/<accountId>/AccessToken`
  * You can then use your token to consume the REST API and automate video indexing tasks, creating projects, retrieving insights, and creating or deleting custom models.
  * For example, a GET call to `https://api.videoindexer.ai/<location>/Accounts/<accountId>/Customization/CustomLogos/Logos/<logoId>?<accessToken>` REST endpoint returns the specified logo.
  * In another example, you can send a GET request to `https://api.videoindexer.ai/<location>/Accounts/<accountId>/Videos?<accessToken>`, which returns details of videos in your account
* Azure Resource Manager (ARM) templates are available to create the Azure AI Video Indexer resource in your subscription, based on the parameters specified in the template file.

-----
# **Azure NLP**

#### Analyze text

* Azure AI Language resource: Language detection, Key phrase extraction, Sentiment analysis, Named entity recognition, Entity linking
* **Detect Language**. Request: "kind": "LanguageDetection", Response "kind": "LanguageDetectionResults"
  * multi-language example response JSON
  `{
    "documents": [
        {
            "id": "1",
            "detectedLanguage": {
                "name": "Spanish",
                "iso6391Name": "es",
                "confidenceScore": 0.9375
            },
            "warnings": []
        }
    ],
    "errors": [],
    "modelVersion": "2022-10-01"
}`

* The last condition to consider is when there is ambiguity as to the language content. The scenario might happen if you submit textual content that the analyzer is not able to parse, for example because of character encoding issues when converting the text to a string variable. As a result, the response for the language name and ISO code will indicate (unknown) and the score value will be returned as 0
* **Key phrase** extraction works best for larger documents (the maximum size that can be analyzed is **5,120 characters**). Extract key phrases - Request: "kind": "KeyPhraseExtraction", Response: "kind": "KeyPhraseExtractionResults"
  `{
         "id": "1",
         "keyPhrases": [
           "change",
           "world"
         ],
         "warnings": []
       }`
* **Sentiment analysis** is used to evaluate how positive or negative a text document is. Sentence sentiment is based on confidence scores for positive, negative, and neutral classification values between 0 and 1. If the sentence classifications include positive and negative, the overall sentiment is mixed. "kind": "SentimentAnalysis", "kind": "SentimentAnalysisResults"
  `{
        "id": "1",
        "sentiment": "positive",
        "confidenceScores": {
          "positive": 0.89,
          "neutral": 0.1,
          "negative": 0.01
        }`
* **Named Entity Recognition** identifies entities that are mentioned in the text.
  * `https://learn.microsoft.com/en-us/azure/ai-services/language-service/named-entity-recognition/concepts/named-entity-categories?tabs=ga-api`
  * "kind": "EntityRecognition", "kind": "EntityRecognitionResults"
  * `"entities":[
                  {
                    "text":"Joe",
                    "category":"Person",
                    "offset":0,
                    "length":3,
                    "confidenceScore":0.62
                  },
                  {
                    "text":"London",
                    "category":"Location",
                    "subcategory":"GPE",
                    "offset":12,
                    "length":6,
                    "confidenceScore":0.88
                  },
                  {
                    "text":"Saturday",
                    "category":"DateTime",
                    "subcategory":"Date",
                    "offset":22,
                    "length":8,
                    "confidenceScore":0.8
                  }
                ]`
* **Extract linked entities:**
  * In some cases, the same name might be applicable to more than one entity. For example, does an instance of the word "Venus" refer to the planet or the goddess from mythology?
  * Entity linking can be used to disambiguate entities of the same name by referencing an article in a knowledge base. Wikipedia provides the knowledge base for the Text Analytics service.
  * "kind": "EntityLinking", "kind": "EntityLinkingResults"
  * `{
        "id": "1",
        "entities": [
          {
            "bingId": "89253af3-5b63-e620-9227-f839138139f6",
            "name": "Venus",
            "matches": [
              {
                "text": "Venus",
                "offset": 6,
                "length": 5,
                "confidenceScore": 0.01
              }
            ],
            "language": "en",
            "id": "Venus",
            "url": "https://en.wikipedia.org/wiki/Venus",
            "dataSource": "Wikipedia"
          }
        ],
        "warnings": []
      }`
   
#### question answering solution
  

-----
## Notes: 

* The task of a conversational language model is to predict the user's intent and identify any entities to which the intent applies. It is not the job of a conversational language model to actually perform the actions required to satisfy the intent. For example, a clock application can use a conversational language model to discern that the user wants to know the time in London; but the client application itself must then implement the logic to determine the correct time and present it to the user.

* Speech Synthesis Markup Language (SSML) enables you to customize the way your speech is synthesized using an XML-based format.

* search solution that consists of the following components:
A data source that references the documents in your Azure storage container.
A skillset that defines an enrichment pipeline of skills to extract AI-generated fields from the documents.
An index that defines a searchable set of document records.
An indexer that extracts the documents from the data source, applies the skillset, and populates the index.

* You need to verify that the person in a photo taken at hospital reception is the same person in a photo taken at a ward entrance 10 minutes later. What should you do?: The most efficient approach is to compare the two faces using the detected face ID within 24 hours.
