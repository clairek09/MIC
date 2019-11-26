# h1
## quiz title: Knowldge Check

## Multiple Choice

Which of the following APIs would be the best choice when making image classification predictions based on custom classification models?
() Custom Vision Training API1 {{The Custom Vision Training API does not provide custom image prediction methods.}}
() Custom Vision Training API {{The Custom Vision Training API does not provide custom image prediction methods.}}
() Computer Vision API {{The Computer Vision API does not provide custom image prediction methods.}}
(x) Custom Vision Prediction API {{The Custom Vision Prediction API is specifically designed to make image classification predictions based on classification models. The Computer Vision and Custom Vision Training APIs do not provide custom image prediction methods.}}

## Multiple Choice

What is the minimum number images required for each tag in order to perform a successful training?
(x) 45 {{Two (2) images per tag is not enough images for a successful training}}
() 4{{To perform a successful training, at least five (5) images are required per tag. The recommended number of images per tag is 30-50, however this exceeds the minimum number that is actually required. Note that two (2) tags are required per image.}}
( ) 40 {{Although 40 images per tag is in the recommended range, it exceeds the minimum required number}}

## Multiple Choice

What is the reported precision value for a model that correctly identifies 96 out of 100 images?
( ) Precise {{The term "Precise" is not a valid precision value.}}
(x) 96% {{When a model correctly identifies 96 out of 100 images, the resulting precision is 96/100, or 96%.}}
( ) Excellent {{The term "Excellent" is not a valid precision value. Precision is reported as a numeric ratio or percentage value, not a qualitative measure of the result.}}

## Multiple Choice

When authorizing requests to the Custom Vision Training API, either via the query string or the request header, which of the following values must be supplied?
( ) Subscription-Key {{A generic "Subscription-Key" value is not used in Microsoft Cognitive Vision Services.}}
(x) Training-key {{Every programmatic call to the Custom Vision Training API requires a Training Key  ("Training-key") to be passed to the service—either via a value in the query string parameter, or specified in the request header. "Prediction-key" is used for the Prediction API, and "Ocp-Apim-Subscription-Key" is used for Computer Vision, Face, and Emotion APIs. A generic "Subscription-Key" value is not used in Microsoft Cognitive Vision Services.}}
( ) Prediction-key {{The "Prediction-key" is used for the Prediction API}}

## Multiple Choice

Which of the following tasks would be a good fit for the Custom Vision API?
( ) Creating a service to identify the formats and color variations in images {{Creating a service to identify image formats and color variations is a built-in feature of the Computer Vision API, and not likely to be an effective use of the Custom Vision API.}}
(x) Creating a service to identify a plant species in images {{The Custom Vision API is designed to identify tagged (classified) elements of any type or characteristic of an image. Creating a service to identify image formats and color variations is built-in feature of the Computer Vision API, and not likely to be an effective use of the Custom Vision API. The Emotion API would be used to evaluate whether the people in an image are happy or sad, and not likely to be an effective use of the Custom Vision API.}}
( ) Creating a service to identify the textual information in images {{Creating a service to extract printed text from an image is a built-in feature of the Computer Vision API, and not likely to be an effective use of the Custom Vision API.}}

## Multiple Choice

Is this a faked question?
( ) Yes, it's my fault. {{This is to check the ' handling}}
(x) No, it has special perpose to test the "'" ? {{This is to check the ' handling}}
( ) Skip your's . {{This is to check the ' handling}}