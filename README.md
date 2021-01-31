# Python-METAR
Python library for aeronautical METAR (METeorological Aerodrome Report). 

## Installation

### PIP

You can use pip in order to install package.

```python
pip install -i https://test.pypi.org/simple/ Python-METAR-MattBOUCHET
```

### Source code

You can also download source code from https://github.com/MatthieuBOUCHET/Python-METAR

Decompress folder and copy `metar/metar.py` in your project folder.

## Usage

### Import

Use 

```python
from Python-METAR import metar
```

### Declare a METAR

#### Retrieve a live METAR

```python
#example = Metar('OACICODE')
example = Metar('LFLY') #Lyon-Bron Airport (LFLY)
```

#### Declare a METAR with data

```python
#example = Metar('ICAOCODE','METARDATAS')
example = Metar('LFQN','METAR LFQN 201630Z 18005KT 4000 -SHRA SCT030 BKN050 18/12 Q1014 NOSIG=') #Saint-Omer Airfield (LFLY)
```

### Get informations

#### List of attributes analyzed

- `airport` (string): ICAO code of METAR airport

- `data_date` (string): Date provided by NOAA server. None if text enter manually

- `metar` (string): Complete METAR message

- `changements` (string) : Changements

- `auto` (boolean): Define if a METAR isfrom an automatic station or not

- `date_time` (tuple): Tuple of date with day, hour & minutes

- `wind` (dictionary): Dictionary with wind information

- `rvr` (tuple): Tuple of dictionaries with RVR information

- `weather` (dictionary): Dictionary of tuple with significant weather information

  \- cloud (tuple): Tuple of dictionaries with cloud detected information

  \- temperatures (dictionary): Dictionary of integers with temperature and dewpoint information

  \- qnh (integer OR float): Information of QNH (integer if hPA, float if inHG)

  \- properties(dictionary): Dictionary of attribute

### Getter

#### All properties

In order to get all properties from METAR, you can use `getProperties()` method.

```python
example = Metar('LFLY') #Lyon-Bron airport
properties = example.getProperties() #Get a dictionnary with all properties
```

If you want to display this dictionary, set `display` argument to True. Default to False

#### An attribute

In order to get one attribute from METAR, you can use `getAttribute(attribute)`method.

List of attributes is available above.

```python
example = Metar('LFLY') #Lyon-Bron airport
properties = example.getAttribute() #Get attribute
```

## Origin of data

Data are provided by NOAA. FTP server is available here : https://tgftp.nws.noaa.gov/data/observations/metar/stations/

## Errors

### NOAAServError

Exception raised if a connection problem encountered during connection with NOAA Servor.

Check your Internet connection & settings.

### ReadingMETARError

Exception raised during parsing METAR with one method. It's a general error.

### ReadFileError

`ReadFileError` is an exception based on Exception basic class. This exception is raised in methods of `Metar` class if an error occurred during reading of file downloaded in temp file by `readlines()` method. Try to execute your program as administrator.