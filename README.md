# Pokemon Tool
Pokemon Tool is a library intended to aid in the acquisition of data from [Smogon](http://www.smogon.com/), and includes methods to search usage data by Pokemon, as well as a few web scrapers to download the Smogon dex in json format.

## Requirements and Dependencies
Pokemon Tool requires you to have Python3 installed, and depends on the following packages:
- [Selenium](https://pypi.python.org/pypi/selenium)
- [BeautifulSoup4](https://pypi.python.org/pypi/beautifulsoup4)

This library also requires read/write permissions to the directory it's located in.

## Installation
### Using Git
In your terminal, navigate to the install destination directory and run:

`git clone https://github.com/luminoray/pokemon-tool.git`

### Zip Download
First, download this project as a zip file (there should be a link to do so on this page). Uncompress the zip file on the location in which you wish you use it.

## Usage
Once properly installed you can use Pokemon Tool by importing it into your project with the following line:

`import pokemontool`

### Functions

`pokemon_usage_dict(date='default', meta='gen7ou', rank=1500)`

Returns a dictionary containing the usage data for the provided **date**, **meta** and **rank**. **date** is in YYYY-MM format. If **date** is set to 'default', it will attempt to get the most recent data.

This will read the data from a json file located in **./stats**. If the file is not available, it will attempt to download it from [Smogon](http://www.smogon.com/stats/). If the information is not available, it will raise a **SmogonError** exception.

Example: `pokemon_usage_dict('2017-02', 'gen7rualpha', rank=1630)`

This function returns the data exactly as it's organized in Smogon.

---

`pokemon(name, date='default', meta='gen7ou', rank=1500)`

Returns a dictionary containing the usage data for the Pokemon with given **name**. The other parameters function exactly as they do in the previous function. If the Pokemon doesn't exist, it will raise a **PokemonError** exception.

This function processes the data obtained from the previous function, and calculates usage percentages.

The dictionary contains the following keys:

- **data** - Contains the usage data as provided from Smogon.
- **Count** - The sum of all the occurrences of Abilities for that Pokemon. Can also be understood as the number of times this Pokemon was used.
- **data_percent** - Contains the usage data in percents.

---

`moves_dict(version='sm')`

Returns a dictionary containing all the move data for the provided **version**. Default is 'sm', referring to Pokemon Sun and Moon.

This will read the data from a json file located in **./dex**. If the file is not available, it will attempt to scrape it from [Smogon](http://www.smogon.com/dex/moves/).

---

`move(name, version='sm')`

Returns a dictionary containing the data for the move with given **name**. **version** behaves just like in the previous function.

You can perform a search either via key or name, case insensitive. For example, if searching for *Shadow Ball*, you can look it up as "Shadow Ball", "shadow ball" or "shadow_ball".

This function returns a value similar to running **moves_dict(version)[_name_to_key(name)]**, but will raise a **MoveError** exception if the key is not found.