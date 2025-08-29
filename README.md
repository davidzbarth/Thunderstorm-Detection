# Thunderstorm-Detection
An algorithm is provided that can point out past thunderstorms from pressure and temperature data alone.\\

## Functionality
This program is supposed to work in a straightforward way:

*detection_of_thunderstorms.ipynb* is the heart of the project. It requires the input of temperature and pressure data in .sac format.
They should stretch over the same time span and obviously contain as much time as possible. 
The resolution in time should be finer than 1 per 10 minutes, ideally much finer.
Those conditions are essential for the algorithm to work.
This data can for example be drawn from seismic stations, which is what I have done. 
iris.edu provides extensive records of those, often including meteorological data.\\

The algorithm takes the data and puts out a .csv file.
It contains the time intervals over which we have continuous data for both temperature and pressure in the first row.
In each column, the file then lists the time intervals where it claims to have found thunderstorms.
Whether this data is output in UCT or local time can be changed at the end of the notebook.\\

How exactly the detection works is explained in detail throughout the notebook.
It can be studied in detail or just used for its main purpose by one "run all".

## Methodology
The algorithm was developed with data from different stations across the United States. 
The challenge was to find finely sampled meteorological data and decent thunderstorm records for one place.

For the finely sampled meteorological data, iris.edu provides extensive records for a lot of stations across the US. 
The IU and II networks are usually reliable.

Finding decent thunderstorm records was harder.
They can be drawn from airport recordings which are easily accessible at https://mesonet.agron.iastate.edu/request/download.phtml 

This combination worked relatively well together although there still are inaccuracies in the data and airport and meteorological station are usually between 15 and 25 kilometers apart from each other.

## Performance
For the stations we calibrated the algorithm with, we got the following performances:

| | Harvard, MA | State College, Pa | Disney Wilderness Preserve, FL | Tucson, AZ | Albuquerque, NM |
|----------|----------|----------|----------|----------|----------|
| True Positives | 59 | 16 | 66 | 218 | 350 |
| Likely True Positives | 17 | 62 | 182 | 85 | 204 |
| False Positives | 22 | 12 | 36 | 115 | 96 |

The absolute numbers depend largely on how frequent thunderstorms are in the specific region and how many years of data we have.
This changes from station to station but overall, we still pick up quite some thunderstorms with a bounded uncertainty.\\

More on what exactly "Likely True Positives" means, can be found in the *benchmark.ipynb* notebook.

## Quick Start to Test
I have included the training data from different stations in the *us_state*.zip files.
They can be downloaded and unpacked and should work with the notebook straight away.
One "Run all" is everything that is needed, as long as the file paths and the time zone is correct.
"LKO" is the channel for the temperature data and "LDO" the one for pressure data in those files.

## Benchmarking
With the *benchmark.ipynb* file, the data can be tested against the airport recordings of thunderstorms.
The latter are included in the compressed folders too.
