## Command Line Usage
The CLI tool is provided mainly for quick tests and debugging.

```shell
# General help
python3 -m mindee -h

# Example command help
python3 -m mindee invoice -h

# Example parse command for Off-the-Shelf document
python3 -m mindee invoice --invoice-key xxxxxxx /path/to/invoice.pdf

# Works with environment variables
export MINDEE_INVOICE_API_KEY=xxxxxx
python3 -m mindee invoice /path/to/invoice.pdf

# Example parse command for a custom document
python3 -m mindee custom -u pikachu -k xxxxxxx pokemon_card /path/to/card.jpg

# You can get the full parsed output as well
python3 -m mindee invoice -o parsed /path/to/invoice.pdf

# In the Git repo, there's a helper script for it
./mindee-cli.sh -h
```
