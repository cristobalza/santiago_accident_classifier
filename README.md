# Santiago, Chile Accident Prediction Classifier

The motivation of this classifier is to provide a solid work that may guide the Santiago, Chile authorities to classify and recognize what, where, and when are the major hot spots when people have lost their lives by engaging in car accidents based on the CONASET data registered by the Chilean police, Carabineros de Chile.

Santiago, Chile is one of the most condensed cities in South America according to [this ranking that puts the city in the 5th place](https://en.wikipedia.org/wiki/List_of_cities_in_South_America). In addition, this article in Spanish gives a ranking of mortality rate in the southern region [here](https://www.reporteindigo.com/latitud/estas-las-ciudades-america-latina-donde-mueren-personas-accidentes-viales/). 

As the U.S. electric car industry [expands at a very fast rate](https://www.iea.org/reports/global-ev-outlook-2020) in several cities around the country, soon will happen the same in South American cities. I think it is imperative for goverments to take serioues accountability in how to prevent in a more efficient way the death of their citizens when the engange in unfortunate vehicle accidents. In most cases accidents are unfortunate, however, I believe that using the power of data we can make better decision on how we can use our resources to do the best we can against the unfortunate destiny.

## Getting Started

Below I'll describe the data used for this project.

### Data Sets

- **Chile's Vector Maps**: This dataset can be download [here](https://www.bcn.cl/obtienearchivo?id=repositorio/10221/10405/2/Areas_Pobladas.zip). This dataset is a zip file __Vector Maps of Chilean cities__. The zip file contains different data format of 387 cities and towns of the Chilean territory. The data was compiled by the [__Chilean National Congress LIbrary (BCN)__](https://www.bcn.cl/), which is a service of the Chilean Senate and the Chamber of Deputies whose mission is "to contribute to the linking of the National Congress of Chile with citizens, giving access to its legal and historical heritage, and promoting instances of dialogue and reflection between parliamentarians and civil society."

- **Santiago's Street Data**:This data can be downloaded by clicking in [this zip file](http://download.geofabrik.de/south-america/chile-latest-free.shp.zip).The dataset was compiled by [__GEOFABRIK__](http://download.geofabrik.de/south-america/chile.html), a community-maintained and free open source database that provides geodata from many different parts of the world that mainly works with free data from [__OpenStreetMap__](https://www.openstreetmap.org/). They are constantly updating, cleaning, and maintaining their databases for free public user access.

    The zip file contains the data of the streets of Chile in different data format. For purpose of this project we will be using `.shp` file.

    [Here](http://download.geofabrik.de/osm-data-in-gis-formats-free.pdf) is a pdf file with the documentation of this data written by Geofabrik. Here the reader can find descriptions of each feature, description of data sources more in details, the relationships of Geofrabik data mining and OpenStreetMap, licenses that guarantees that this is a free source of data, the meaning of each feature class, among others. We use the pdf file to guide us in understanding how the data was compiled for us and understand the language they use to name their data's features. 

- **The Motorized Vehicles accidents was compiled by [__CONASET__](http://mapas-conaset.opendata.arcgis.com/) a Chilean goverment department of transit security**: This dataset was elaborated with the help of [__Carabineros de Chile__](https://en.wikipedia.org/wiki/Carabineros_de_Chile), they are the national police department of Chile. In other words, Carabineros de Chile record the data since they are the ones who are present after an accident happens and then the data is take to CONASET to be processed and file

    The datasets consist the registered list of accidents in the years 2015-2018. All accidents involve cars somehow.

    It can be downloaded as zip files here:
    - [2015](https://opendata.arcgis.com/datasets/dafa26dbce99467985596d8a58216b79_0.zip)
    - [2016](https://opendata.arcgis.com/datasets/32ee49c703b840b885b9c80b37ae72d0_0.zip)
    - [2017](https://opendata.arcgis.com/datasets/907addac92b74e3fa30d40edb72d1813_0.zip)
    - [2018](https://www.arcgis.com/sharing/rest/content/items/ff520ff145614d5585f9905892e48957/data) 
- **2017 Chilean Census Data**: The data can be downloaded [here](https://www.bcn.cl/siit/estadisticasterritoriales/tema?id=168). We will use the Census data to normalize our Accidents data better. 

    This dataset was also obtained from the BCN (same source as the Vector Maps).

### Prerequisites

Things you need to know or get installed in your machine in order to recreate this project or do something similar:

- Know how to navigate your machine Terminal 

- Have installed Anaconda package manager and Jupyter Notebooks in your machine.

- Software you need to get installed in your machine:

```
appnope==0.1.0
attrs==19.3.0
backcall==0.2.0
certifi==2020.6.20
click==7.1.2
click-plugins==1.1.1
cligj==0.5.0
cycler==0.10.0
decorator==4.4.2
Fiona==1.8.13.post1
geopandas==0.8.1
ipykernel==5.3.4
ipython==7.17.0
ipython-genutils==0.2.0
jedi==0.17.2
Jinja2==2.11.2
joblib==0.16.0
jupyter-client==6.1.6
jupyter-core==4.6.3
kiwisolver==1.2.0
MarkupSafe==1.1.1
matplotlib==3.3.1
munch==2.5.0
numpy==1.19.1
pandas==1.1.0
parso==0.7.1
pexpect==4.8.0
pickleshare==0.7.5
Pillow==7.2.0
pipdeptree==1.0.0
prompt-toolkit==3.0.6
ptyprocess==0.6.0
Pygments==2.6.1
pyparsing==2.4.7
pyproj==2.6.1.post1
python-dateutil==2.8.1
pytz==2020.1
pyzmq==19.0.2
scikit-learn==0.23.2
scipy==1.5.2
seaborn==0.10.1
Shapely==1.7.0
six==1.15.0
sklearn==0.0
threadpoolctl==2.1.0
tornado==6.0.4
traitlets==4.3.3
wcwidth==0.2.5
```

However, you can do the following steps to recreate the software environment of this project into your machine:

1. Create a conda environment. Run the following command in your project directory `conda create —name [YOUR PROJECT ENVIRONMENT] —file requirements.txt`. The `requirements.txt` you can find in the repository and contains the above software and correspoding versions.

2. Activate the environment. Run `conda activate [YOUR PROJECT ENVIRONMENT]`

3. Create a new Kernel in your Jupyter Notebook. First, run `pip install ipykernel` to intall or check if you have installed this package manager in `python -m ipykernel install --user --name [YOUR PROJECT ENVIRONMENT] --display-name "SOME NAME THAT YOU LIKE FOR YOUR KERNEL. E.G.: Python 3.7 (Santiago Project)"`

4. Go to your Terminal and run `jupyter notebook` to open the jupyter notebooks in your local host. Then when you create a new Python file make sure to select the new Kernel created.

The reason of creating a new Anaconda environment and Jupyter Kernel is to have a clean new "workplace" for us to install and uninstall new packages and explore new technologies without messing with other packages that we may have somewhere else in our computers.





## Acknowledgments

* Original idea of this project was taken for [How safe are the streets of Santiago?](https://towardsdatascience.com/how-safe-are-the-streets-of-santiago-e01ba483ce4b), an article written by a Chilean Professor who does an exploratory analysis of Santiago's accidents of 2018 using GeoPandas. This project contains a superset of that article's dataset and some snippets of code from the article. However, we have included a much wider and diverse datasets. This disclaimer's purpose is to give credit to the inspiration of this project and by no means this project objective is the same as the article. The intention of this project is to apply the Data Science Lifecycle and Machine Learning  algorithms to make decisions in the future on how we can start thinking in effective policies to prevent deathly car accidents.

* Use [this template](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2) to write this documentation