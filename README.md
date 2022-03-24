<p align="center">
  <img src="docs/kids_first_logo.svg" alt="Kids First repository logo" width="660px" />
</p>
<p align="center">
  <a href="https://github.com/kids-first/kf-template-repo/blob/master/LICENSE"><img src="https://img.shields.io/github/license/kids-first/kf-template-repo.svg?style=for-the-badge"></a>
</p>

# Instructions to run test ingest package

Run a test ingest package

## Python Noe

Make sure that you are running *at least* python v3.6 or greater.

## Instal the ingest library and the ingest package repo

### Setup virtual environment (optional but recommended)

I'd suggest running the ingest library inside a virtual environment

```sh
python3 -m venv venv
source ./venv/bin/activate
```

### Install the Ingest Library
<!-- markdownlint-disable MD034 -->
'''sh
pip install psycopg2-binary
pip install git+https://github.com/kids-first/kf-lib-data-ingest.git@latest-release
'''
<!-- markdownlint-enable MD034 -->

### Install the ingest package repo

'''sh
git clone git@github.com:kids-first/kf-ingest-package-demo.git
'''

## Run the test ingest package

`cd` into the test ingest package

```sh
cd kf-ingest-package-demo/SD_ME0WME0W
```

### Make sure that the target dataservice has the study you're ingesting

try to curl the study in your target dataservice.

From here on out, i'm using the localhost:5000 as the target
dataservice url. Make sure to replace that value with the appropriate url.

```sh
curl http://localhost:5000/studies/SD_ME0WME0W 
```

If that returns a bunch of information about a study, move on to the next step.

if that returns a 404, you'll need to create the study in your target
dataservice:

```sh
curl -XPOST -H "Content-Type: application/json" http://localhost:5000/studies \ 
-d '{"attribution":"Hamburgerz","data_access_authority":"dbGaP","domain":"OTHER","external_id":"CHEEZBURGER","kf_id":"SD_ME0WME0W","name":"Mr. Meows Memorable Meme Emporium \ud83d\uddbc","program":"MEOW","release_status":null,"short_code":"MEOW-MEOW","short_name":"Cat Pics","version":"PLZ","visible":true}'
```

### Make sure that the target dataservice has the sequencing center you're ingesting to

try to curl the study in your target dataservice.

From here on out, i'm using the QA KidsFirst Dataservice as the target
dataservice url. Make sure to replace that value with the appropriate url.

```sh
curl http://localhost:5000/sequencing-centers/SC_CATTVETT 
```

If that returns a bunch of information about a sequencing center, move on to
the next step.

if that returns a 404, you'll need to create the study in your target
dataservice:

```sh
curl -XPOST -H "Content-Type: application/json"  http://localhost:5000/sequencing-centers -d '{"kf_id":"SC_CATTVETT", "name":"Feline Diagnostics", "visible": "True"}'
```

## Run the ingest package

run the following to ingest files into your target dataservice (remember to
change the url that of yours!)

```sh
kidsfirst ingest . -t http://localhost:5000
```
