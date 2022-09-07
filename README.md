# Free-form Artwork Images Inpainting Using a Self-Supervised CNN-Based Autoencoder

1. Project Description and motivation:

Create a useful tool for deep learning-based inpainting model of artworks, for restoration purpose or digital presentation purpose in museums/art galleries. This model was initially trained on over 100,000 artwork images but is also designed to be easily trainable without requiring expensive computation settings and time. Therefore, art restorators can re-train the model on specific datasets to gain better predictions on specific types of artworks. The self-supervised part is completed by pre-training the encoder with contrastive learning, which is used to enrich the embedding by associating similar images together.

Artworks get damaged over time and it is art conservators' task to restore artworks. Human restoration is very time consuming and sometimes is subjected to human error, but it can lead to very good results like the image below:
<img width="748" alt="image" src="https://user-images.githubusercontent.com/82073987/188959014-65bb3e0c-93cb-4f1e-8888-5a89c153f1c7.png">

However, there are examples of bad restorations like:
<img width="732" alt="image" src="https://user-images.githubusercontent.com/82073987/188959165-26c7eef9-2109-4551-b252-5c7d79e62a2a.png">

To aid and speed up the tasks of art conservators, our model is trained to complete the free-form inpainting as shown in the image below:
<img width="667" alt="image" src="https://user-images.githubusercontent.com/82073987/188959326-04b25740-43d5-4308-a528-d8645a4cc030.png">


2. Data Loading and processing:

- Links to training dataset:
Raw data: https://raw.githubusercontent.com/NationalGalleryOfArt/opendata/main/data/published_images.csv

The github: https://github.com/NationalGalleryOfArt/opendata/tree/main/data

- Links to datasets from which test images have been extracted by category:
https://rusmuseumvrm.ru/collections/index.php?lang=en

https://artchallenge.ru/?lang=en

https://www.kaggle.com/datasets/ikarus777/best-artworks-of-all-time

https://www.kaggle.com/datasets/thedownhill/art-images-drawings-painting-sculpture-engraving

Import the csv file with URLs into Jupyter Notebook as a pandas dataframe with the image URLs and IDs. After which the images are downloaded locally for processing. A data cleaning process is applied to get rid of all the images that have one dimension smaller than 128 pixels. Then, the images are centre-cropped to 128x128 pixels. But it's important to note the images for the testing dataset are manually extracted from online datasets and divided into four categories: abstract images, pencil drawings, paintings of people, and paintings of landscape.

The free-form masks (random series of strokes of different length and different thickness separated by random angles) are the regions our model will have to reconstruct. They are part of the image processing but are only applied during runtime in a random manner. Each masks are generated randomly with random design to ensure our model does not learn any masking patterns. This keeps our model versatile to different types of restoration.
