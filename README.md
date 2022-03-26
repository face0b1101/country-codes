# Country-Codes

[![goodtables.io](https://goodtables.io/badge/github/datasets/country-codes.svg)](https://goodtables.io/github/datasets/country-codes)

Comprehensive country code information, including ISO 3166 codes, ITU dialing
codes, ISO 4217 currency codes, and many others. Provided as a [Tabular Data Package](http://frictionlessdata.io/data-packages/): [view datapackage](http://data.okfn.org/tools/view?url=https%3A%2F%2Fraw.githubusercontent.com%2Fdatasets%2Fcountry-codes%2Fmaster%2Fdatapackage.json)

## Data

Data is fetched from multiple sources:

Official formal and short names (in English, French, Spanish, Arabic, Chinese, and Russian) are from
[United Nations Protocol and Liaison Service](https://protocol.un.org/dgacm/pls/site.nsf/PermanentMissions.xsp)

Customary English short names are from
[Unicode Common Locale Data Repository (CLDR) Project](https://github.com/unicode-cldr/cldr-localenames-full/blob/master/main/en/territories.json).

Note: CLDR shorter names "ZZ-alt-short" are used when available

ISO 3166 official short names (in English, French, Spanish, Arabic, Chinese, and Russian) are from
[United Nations Department of Ecoonomic and Social Affairs Statistics Division](https://unstats.un.org/unsd/methodology/m49/overview/)

ISO 4217 currency codes are from
[currency-iso.org](https://www.currency-iso.org/dam/downloads/lists/list_one.xml)

Many other country codes are from
[statoids.com](http://www.statoids.com/wab.html)

Special thanks to Gwillim Law for his excellent
[statoids.com](http://www.statoids.com) site (some of the field descriptions
are excerpted from his site), which is more up-to-date than most similar
resources and is much easier to scrape than multiple Wikipedia pages.

Capital cities, languages, continents, TLDs, and geonameid are from [geonames.org](http://download.geonames.org/export/dump/countryInfo.txt)

EDGAR codes are from [sec.gov](https://www.sec.gov/edgar/searchedgar/edgarstatecodes.htm)

## Preparation

This package includes Python scripts to fetch current country information
from various data sources and output CSV of combined country code information.

CSV output is provided via the `in2csv` and `csvcut` utilities from [csvkit](http://github.com/onyxfish/csvkit)

Currently, preparation requires manual process to download and rename 6 CSV files from https://unstats.un.org/unsd/methodology/m49/overview/

*TODO: automate the downloads*

Download and place in the `{project_root}/source` directory:

* `source/UNSD-en.csv`
* `source/UNSD-fr.csv`
* `source/UNSD-ar.csv`
* `source/UNSD-cn.csv`
* `source/UNSD-es.csv`
* `source/UNSD-ru.csv`

### Docker

Use docker to create a container that does all the messy work for you.
Navigate to the root of this project, then run the following:

```bash
docker build -t country_codes ./scripts;
docker run --rm \
--name country_codes \
-v $PWD:/country_codes \
-w /country_codes \
country_codes \
make country-codes.csv
```

### data/country-codes.csv

Or, do it the old fashioned way...
Install requirements:

```bash
pip install -r scripts/requirements.pip
```

Run GNU Make to generate data file:

```bash
make country-codes.csv
```

## License

This material is licensed by its maintainers under the Public Domain Dedication
and License.

Nevertheless, it should be noted that this material is ultimately sourced from
ISO and other standards bodies and their rights and licensing policies are somewhat
unclear. As this is a short, simple database of facts there is a strong argument
that no rights can subsist in this collection. However, ISO state on [their
site](http://www.iso.org/iso/home/standards/country_codes.htm):

> ISO makes the list of alpha-2 country codes available for internal use and
> non-commercial purposes free of charge.

This carries the implication (though not spelled out) that other uses are not
permitted and that, therefore, there may be rights preventing further general
use and reuse.

If you intended to use these data in a public or commercial product, please
check the original sources for any specific restrictions.
