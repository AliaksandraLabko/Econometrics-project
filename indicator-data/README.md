- [Introduction](#introduction)
- [License](#license)
- [Contact information](#contact-information)
- [Archive Content](#archive-content)

# Introduction
This archive consists of the data (and optionally metadata) returned from the indicator data export API. See the [API documentation](https://api.uis.unesco.org/api/public/documentation/operations/exportIndicatorData) for details on the usage and options.

# License

The data is licensed under the [Creative Commons Attribution-ShareAlike 4.0 International](https://creativecommons.org/licenses/by-sa/4.0/) license.

Visit the [Terms and conditions page](https://databrowser.uis.unesco.org/terms-and-conditions) for more information.

# Contact information
If you have any questions or comments about this archive please contact us at:

```
UNESCO Institute for Statistics
3500 De Maisonneuve Boulevard West, RS-1100
Montreal, Quebec, Canada H3Z 3C1
Tel: +1 514 343 6880
Email: uis.datarequests@unesco.org
```

# Archive Content
This archive contains the following files:

## data.csv
This file contains a list of data records of the requested dataset.

File structure:

| Column Name | Description                                                                                                                                                                                                      |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| indicatorId | The indicator code of the measured value. See `indicators.csv` file for the definition of the disaggregations (match via `indicatorId` field).                                                                   |
| geoUnit     | GeoUnit id (country or region id) of the measured value. See [geo unit definitions endpoint](https://api.uis.unesco.org/api/public/documentation/operations/listGeoUnits) for a list and names of all geo units. |
| year        | Year of the measured value                                                                                                                                                                                       |
| value       | Measured value                                                                                                                                                                                                   |
| qualifier   | Metadata describing the QUALITY of the measured value.  [Definition of Qualifier](https://api.uis.unesco.org/api/public/documentation/schemas/Qualifier).                                                        |
| magnitude   | Metadata describing the NATURE of the measured value.  [Definition of Magnitude](https://api.uis.unesco.org/api/public/documentation/schemas/Magnitude).                                                         |

NOTE: The `footnotes.csv` file only exists when the `footnotes` parameter was set to `true` when requesting data. The `indicators.csv` and `disaggregations.csv` files are optional and only exist if the `indicatorMetadata` parameter was set to `true` when requesting the data.

## footnotes.csv (optional)
Optional file, only exists if the `footnotes` parameter is set to `true` when fetching data.

This file contains a list of all data points level footnotes of the requested dataset. Matching of footnotes to data points is done via the `indicatorId`, `geoUnit`, and `year` fields combined.

File structure:

| Column Name | Description                                                                                                                                                                                                      |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| indicatorId | The indicator code of the measured value. See `indicators.csv` file for the definition of the disaggregations (match via `indicatorId` field).                                                                   |
| geoUnit     | GeoUnit id (country or region id) of the measured value. See [geo unit definitions endpoint](https://api.uis.unesco.org/api/public/documentation/operations/listGeoUnits) for a list and names of all geo units. |
| year        | Year of the measured value                                                                                                                                                                                       |
| type        | See [Footnote model definition](https://api.uis.unesco.org/api/public/documentation/schemas/Footnote) for details and examples.                                                                                  |
| subtype     | See [Footnote model definition](https://api.uis.unesco.org/api/public/documentation/schemas/Footnote) for details and examples.                                                                                  |
| value       | Footnote value. See [Footnote model definition](https://api.uis.unesco.org/api/public/documentation/schemas/Footnote) for details and examples.                                                                  |

## indicators.csv (optional)
Optional file, only exists if the `indicatorMetadata` parameter is set to `true` when fetching data.

This file contains a list of all indicators contained in the dataset.

File structure:

| Column Name                       | Description                                                                                                                                                                   |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| indicatorId                       | Indicator code                                                                                                                                                                |
| name                              | Indicator code English label                                                                                                                                                  |
| theme                             | The theme to which the indicator belongs. [Definition of Themes](https://api.uis.unesco.org/api/public/documentation/schemas/Theme).                                          |
| lastDataUpdate                    | Date of the last data update for this indicator.                                                                                                                              |
| lastDataUpdateDescription         | Short description of the last data update for this indicator.                                                                                                                 |
| disaggregations                   | List of disaggregations (comma-separated) associated with this indicator. See `disaggregations.csv` file for the definition of the disaggregations (match via `code` column). |
| glossaryTerms                     | List of glossary terms associated with this indicator. See `glossary-terms.csv` file for the definition of the disaggregations (match via `termId` column).                   |
| dataAvailability.totalRecordCount | See [IndicatorDataAvailabilityInfo model definition](https://api.uis.unesco.org/api/public/documentation/schemas/IndicatorDataAvailabilityInfo) for details.                  |
| dataAvailability.timeLine.min     | See [IndicatorDataAvailabilityInfo model definition](https://api.uis.unesco.org/api/public/documentation/schemas/IndicatorDataAvailabilityInfo) for details.                  |
| dataAvailability.timeLine.max     | See [IndicatorDataAvailabilityInfo model definition](https://api.uis.unesco.org/api/public/documentation/schemas/IndicatorDataAvailabilityInfo) for details.                  |
| dataAvailability.geoUnits.types   | See [IndicatorDataAvailabilityInfo model definition](https://api.uis.unesco.org/api/public/documentation/schemas/IndicatorDataAvailabilityInfo) for details.                  |

## disaggregations.csv (optional)
Optional file, only exists if the `indicatorMetadata` parameter is set to `true` when fetching data.

This file contains a list of all disaggregations contained used by any indicator in the dataset.

File structure:

| Column Name               | Description                                                                                                                                 |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| code                      | Disaggregation code                                                                                                                         |
| name                      | See [DisaggregationType model definition](https://api.uis.unesco.org/api/public/documentation/schemas/DisaggregationType) for details.      |
| description               | See [DisaggregationType model definition](https://api.uis.unesco.org/api/public/documentation/schemas/DisaggregationType) for details.      |
| glossaryTerms             | See [DisaggregationType model definition](https://api.uis.unesco.org/api/public/documentation/schemas/DisaggregationType) for details.      |

## glossary-terms.csv (optional)
Optional file, only exists if the `indicatorMetadata` parameter is set to `true` when fetching data.

This file contains a list of all glossary terms associated with any indicator or disaggregation in the dataset.

File structure:

| Column  Name          | Description                                                                                                                             |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| termId                | Id of the glossary term.                                                                                                                |
| name                  | Glossary term name.                                                                                                                     |
| definition            | See [GlossaryTerm model definition](https://api.uis.unesco.org/api/public/documentation/schemas/GlossaryTerm) for details and example.  |
| definitionSource      | See [GlossaryTerm model definition](https://api.uis.unesco.org/api/public/documentation/schemas/GlossaryTerm) for details and example.  |
| purpose               | See [GlossaryTerm model definition](https://api.uis.unesco.org/api/public/documentation/schemas/GlossaryTerm) ffor details and example. |
| calculationMethod     | See [GlossaryTerm model definition](https://api.uis.unesco.org/api/public/documentation/schemas/GlossaryTerm) for details and example.  |
| dataRequired          | See [GlossaryTerm model definition](https://api.uis.unesco.org/api/public/documentation/schemas/GlossaryTerm) for details and example.  |
| dataSource            | See [GlossaryTerm model definition](https://api.uis.unesco.org/api/public/documentation/schemas/GlossaryTerm) for details and example.  |
| typesOfDisaggregation | See [GlossaryTerm model definition](https://api.uis.unesco.org/api/public/documentation/schemas/GlossaryTerm) for details and example.  |
| interpretation        | See [GlossaryTerm model definition](https://api.uis.unesco.org/api/public/documentation/schemas/GlossaryTerm) for details and example.  |
| qualityStandards      | See [GlossaryTerm model definition](https://api.uis.unesco.org/api/public/documentation/schemas/GlossaryTerm) for details and example.  |
| limitations           | See [GlossaryTerm model definition](https://api.uis.unesco.org/api/public/documentation/schemas/GlossaryTerm) for details and example.  |