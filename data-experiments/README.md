# Data Science - Utilities

Running Dask scheduler & worker:

```bash
docker run --name dask-scheduler --rm -d -p 8786:8786 -p 8787:8787 daskdev/dask:2022.2.1-py3.9 dask-scheduler
docker run --name dask-worker --rm -d daskdev/dask:2022.2.1-py3.9 dask-worker host.docker.internal:8786
```

## altermarkive/csv-aggregate

This script statistically aggregates a CSV file.

    docker run --rm -it -v $PWD:/data altermarkive/csv-aggregate CSV_RAW CSV_AGGREGATED INDEX_COLUMN AGGREGATION_JSON


## altermarkive/csv-concatenate

This script concatenates two CSV files.

    docker run --rm -it -v $PWD:/data altermarkive/csv-concatenate CSV_1 CSV_2 ... CSV_CONCATENATED


## altermarkive/csv-interpolate

This script interpolates across gaps in a column.

    docker run --rm -it -v $PWD:/data altermarkive/csv-interpolate CSV_FILE_IN CSV_FILE_OUT COLUMN_REFERENCE COLUMN_IN COLUMN_OUT


## altermarkive/csv-join

This script joins columns in CSV file.

    docker run --rm -it -v $PWD:/data altermarkive/csv-join  CSV_FILE_IN CSV_FILE_OUT DELIMITER COLUMN_1 COLUMN_2 ... COLUMN_JOINED


## altermarkive/csv-rename

This script renames columns in CSV file.

    docker run --rm -it -v $PWD:/data altermarkive/csv-rename CSV_FILE_IN CSV_FILE_OUT COLUMN_1_FROM COLUMN_2_FROM ... COLUMN_1_TO COLUMN_2_TO ...


## altermarkive/csv-select

This script selects columns in CSV file.

    docker run --rm -it -v $PWD:/data altermarkive/csv-select CSV_FILE_IN CSV_FILE_OUT COLUMN_1 COLUMN_2 ...


## altermarkive/csv-split-by-time-of-day

This script splits the value from a given column into separate ones depending on time of day (night, morning, afternoon, evening).

    docker run --rm -it -v $PWD:/data altermarkive/csv-split-by-time-of-day CSV_FILE_IN CSV_FILE_OUT TIMESTAMP_COLUMN SPLIT_COLUMN_1 ...


## altermarkive/csv-timestamp-from-local

This script converts local date/time to UNIX-epoch timestamp in a CSV file.

    docker run --rm -it -v $PWD:/data altermarkive/csv-timestamp-from-local CSV_FILE_IN CSV_FILE_OUT COLUMN_FROM COLUMN_TO PATTERN


## altermarkive/csv-timestamp-range-label

This script labels a column depending on given timestamp ranges.

    docker run --rm -it -v $PWD:/data altermarkive/csv-timestamp-range-label CSV_FILE_IN CSV_FILE_OUT TIMESTAMPS CSV_FILE_LABELS TIMESTAMPS_BEGIN TIMESTAMPS_END COLUMN_FROM_1 COLUMN_LABEL_DEFAULT_1 COLUMN_LABEL_FROM_1 COLUMN_TO_1 ...


## altermarkive/csv-timestamp-to-local

This script converts UNIX-epoch timestamp to local date/time in a CSV file.

    docker run --rm -it -v $PWD:/data altermarkive/csv-timestamp-to-local CSV_FILE_IN CSV_FILE_OUT COLUMN_FROM COLUMN_TO PATTERN


## altermarkive/csv-timestamp-to-season

This script converts UNIX-epoch timestamp to season in a CSV file.

    docker run --rm -it -v $PWD:/data altermarkive/csv-timestamp-to-season CSV_FILE_IN CSV_FILE_OUT COLUMN_FROM COLUMN_TO SPRING_NAME SUMMER_NAME AUTUMN_NAME WINTER_NAME


## altermarkive/csv-timestamp-to-weekend

This script converts UNIX-epoch timestamp to weekend in a CSV file.

    docker run --rm -it -v $PWD:/data altermarkive/csv-timestamp-to-weekend CSV_FILE_IN CSV_FILE_OUT COLUMN_FROM COLUMN_TO


## altermarkive/plot-boxplot-grouped

This script creates a box plot for the given value and group columns.

    docker run --rm -it -v $PWD:/data altermarkive/plot-boxplot-grouped CSV_FILE_IN PNG_FILE_OUT COLUMN_VALUES COLUMN_GROUPS


## altermarkive/plot-boxplot-versus

This script creates a box plot for given columns.

    docker run --rm -it -v $PWD:/data altermarkive/plot-boxplot-versus CSV_FILE_IN PNG_FILE_OUT COLUMN_1 ...


## altermarkive/plot-heatmap

This script creates a heatmap plot.

    docker run --rm -it -v $PWD:/data altermarkive/plot-heatmap '{"input_file": "correlation.csv", "output_file": "figure.png", "cmap_name": "RdBu_r", "title": "Feature Correlation"}'


## altermarkive/plot-pairplot-sampled

This script creates a sampled pair plot.

    docker run --rm -it -v $PWD:/data altermarkive/plot-pairplot-sampled '{"input_file": "/data/data.csv", "output_file": "/data/figure.png", "n": 1000, "class_column": "target", "feature_columns": "^feature"}'


## altermarkive/plot-scatterplot

This script creates a scatter plot for given columns.

    docker run --rm -it -v $PWD:/data altermarkive/plot-scatterplot CSV_FILE_IN PNG_FILE_OUT COLUMN_X COLUMN_Y


## altermarkive/plot-violinplot-per-feature-per-class

This script creates a violin plot.

    docker run --rm -it -v $PWD:/data altermarkive/plot-scatterplot '{"input_file": "data.csv", "output_file": "figure.png", "feature_columns": "^feature", "class_column": "target"}'

## altermarkive/stat-correlation

This script computes pairwise correlation of columns. For example:

    docker run --rm -it -v $PWD:/data altermarkive/stat-correlation '{"input_file": "input.csv", "output_file": "correlation.csv", "columns": ["feature1", "feature2"]}'