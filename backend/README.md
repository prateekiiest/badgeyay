# Badgeyay Backend

> **Badgeyay provide an interface to event organizers for generating badges of events from concerts to conferences and meet-ups.**

Badgeyay is a Badge generator with a simple web UI to add data and generate printable badges in a PDF.

## Data model

### Request

`/api/v1.0/generate_badges`
- Method: POST
- Parameters:
   - custfont: Font to use. if it is null or not present the default font will be used.
   - file: .csv which contains user data
   - csv: CSV data as plain text seperated by a comma (,)
   
   (Either file or csv must be present in the query if both are present, file will be processed)
   - img-default: The dafault image to use. (Required)
   - bg_color: Hex code of background colour of the badge. Will only be parsed if the value of img-default is "user_defined.png"
   - image: The custom background image (in .png format) of the badge which will be uploaded
   
   (Either img-default or image must be present in the query if both are present, image will be processed)

### Response

```json
[{
"type" : "success",
"message" : "pdf generation completed successfully",
"download_link" : "https://badgeyay-dev.herokuapp.com/static/badges/team-png-csv-badges.pdf"
}]
```

## Prerequisites

Badgeyay backend requires the following dependencies to be installed.
   - python3

    - For Ubuntu/Debian based Package Managers
      *  `sudo apt-get update`
      *  `sudo apt-get install python3`
  
    - For Fedora/CentOS/RPM based package managers
      *   `sudo -i`
      *   `yum install python3`
      *   `exit`

    - For Arch based package managers:
      *   `sudo pacman -S python-cairosvg`
      *   `sudo pacman -S python-lxml`

## Installation

Badgeyay backend can be easily deployed on a variety of platforms. Currently it can be deployed in following ways.

1. [Local Installation using Virtual environment](docs/installation/localvir.md)

2. [Local Installation using Vagrant environment](docs/installation/localvag.md)

3. [Deployment on Heroku](docs/installation/heroku.md)

4. [Deployment with Docker](docs/installation/docker.md)

One-click Docker, Heroku, Scalingo and Bluemix deployment is also available:

[![Deploy to Docker Cloud](https://files.cloud.docker.com/images/deploy-to-dockercloud.svg)](https://cloud.docker.com/stack/deploy/?repo=https://github.com/fossasia/badgeyay) [![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/fossasia/badgeyay/tree/development) 
[![Deploy on Scalingo](https://cdn.scalingo.com/deploy/button.svg)](https://my.scalingo.com/deploy?source=https://github.com/fossasia/badgeyay#development) 
[![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/fossasia/badgeyay&branch=development)


## Testing Methodology Used

* [Python Unit tests](https://docs.python.org/3/library/unittest.html).

> The guidelines for setting up and running the tests are mentioned in the [Testing docs](docs/test/testing.md).

## Working

### Input

- The input can be a set of csv files(UTF-8) or a manual entry.
- Detailed Information on Correct format of Input can be found at [Badgeyay User-Input Guide](http://badgeyay.com/#/guide).

### Implementation

- [generate_badges.py](app/generate_badges.py) creates svg files from the `csv`, `png`.
- [badges/8BadgesOnA3.svg](badges/8BadgesOnA3.svg).
- [merge_badges.py](app/merge_badges.py) converts them into pdf files and merges them together into one.

### Output

- The output file is pdf of size A3.
- Each badge has the size A6.
- The outputs are in a folder derived from the input csv.

### Customization

- You can change the font style, font size, color etc from the `.svg` file in the folder badges.
- Inkscape is generally used for editing of such files.
