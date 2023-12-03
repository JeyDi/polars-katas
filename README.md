<h1 align="center">🐻‍❄️ Polars Katas</h1>

<div align="center">
    <i>
        In data's embrace,<br>
        Polars' dance, a swift, fine art,<br>
        Mastery's soft grace.
    </i>
</div>

---

![polar-youngling](./public/polars-katas.png)

## 🍱 Preparations for this journey

1. Install [`PDM`](https://pdm-project.org/latest/#recommended-installation-method) or any other PEP-517 PEP-518 compliant package manger (basically, not `poetry`).

> **Note**
>
> **Recommended way to install Python CLIs**
>
> `pip install [--user] <lib>` can mess up with your system python (even when used with the `--user` flag).
> It is better to use a tool such as `pipx`, that will install every executable in a sandboxed environment.

```bash
pipx install pdm
```

2. Install the dependencies

```bash
# basically, just installs polars
pdm install

# install jupyter as well
pdm install -G ide
```

3. Launch an IDE, a REPL or a Jupyter notebook to run the katas. Execute the following cell to import Polars and a list of URLs that contain the data. We'll use the NYC Taxi dataset. We can get the links of the data from February to September 2023 only, since they have the same format. The source is [here](https://www1.nyc.gov/site/tlc/about/tlc-trip-record-data.page).

```python
import polars as pl

base = "https://d37ci6vzurychx.cloudfront.net/trip-data/yellow_tripdata_2023-{:02d}.parquet"

# we keep the files from Feb 2023 to retain those with the same schema
urls = tuple(base.format(month) for month in range(2, 10))
```

## White Belt: Reading Data

### Kata 1: Eager Mode

* Read the first parquet file in the list using `pl.read_parquet`.
* Display the top five rows.

How long does this take?

<details>
<summary>Solution</summary>

```python
import polars as pl

url = urls[0]

pl.read_parquet(url).head()
```
</details>

### Kata 2: Lazy mode

Repeat the exercise above, using `pl.scan_parquet` instead. What happens if you run the code? What changes if you scan the whole set of URLs?

Write the code to materialize the result.

<details>
<summary>Solution</summary>

```python
pl.scan_parquet(url).head().collect()

pl.scan_parquet(urls).head()
```
</details>

```python
import polars as pl

url = urls[0]

pl.scan_parquet(0).head().collect()
```
</details>


