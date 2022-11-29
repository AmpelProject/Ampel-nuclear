# Ampel-ZTFbh
Central repository to host private AMPEL code from the ZTFbh SWG.

## Installation
### Prerequisites
You need to export environment variables for the [AMPEL ZTF archive](https://ampelproject.github.io/astronomy/ztf/index) (tokens are available [here](https://ampel.zeuthen.desy.de/live/dashboard/tokens)), for the dropbox API and for [Fritz](https://fritz.science/).

Furthermore, you need a running instance of [MongoDB](https://www.mongodb.com/docs/manual/installation/).

### Setup
Create a fresh Python 3.10 conda env
```
conda create -n tde_filter_upgrade python=3.10
conda activate tde_filter_upgrade
```
Install is done via poetry:
```
pip install poetry 
git clone https://github.com/AmpelProject/ampel-nuclear
cd Ampel-nuclear
poetry install
```
Now we have to build the ampel config. Issue
```
ampel config build -out ampel_conf.yaml
```
Now you need to export the following tokens
```
export AMPEL_ARCHIVE_TOKEN, DROPBOX_TOKEN and FRITZ_TOKEN
```
To run the test, issue
`./run_tde_test.py -i`
The `-i` initiates a new stream token. To change the date, use `-d YYYY-MM-DD` for a certain day. The script will request alerts for the 24 hours after this date.
Note: When requesting a full day with `-d` from the archive, the first run will probably fail, as it's not ready yet (`URL is locked`). Just rerun `./run_tde_test.py -d YYYY-MM-DD` in that case until it works.

To check the output, go to the `temp` directory that gets created when script is run without `-p` (push to dropbox).