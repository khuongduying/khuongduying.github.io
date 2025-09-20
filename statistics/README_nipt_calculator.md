# NIPT Risk Calculator Usage Guide

## Quick Start

### Basic Usage
```bash
python3 nipt_risk_calculator.py abnormal.tsv
```

### With Output File
```bash
python3 nipt_risk_calculator.py abnormal.tsv --output results.csv
```

### With Report Generation
```bash
python3 nipt_risk_calculator.py abnormal.tsv --output results.csv --report
```

## Input Format

The script expects a TSV (Tab-Separated Values) file with the following columns:
- `sample`: Sample identifier
- `chr13`: Z-score for chromosome 13
- `chr18`: Z-score for chromosome 18  
- `chr21`: Z-score for chromosome 21

Example input format:
```
sample	chr13	chr18	chr21
Sample1	-0.22	-3.08	-0.067
Sample2	-0.82	-2.06	-1.003
```

## Output Format

The script generates a CSV file with the following columns for each trisomy (T13, T18, T21):
- `{trisomy}_probability_pct`: Risk percentage (0-100%)
- `{trisomy}_ratio`: Risk in ratio format (e.g., "1/1000" or ">1/20")
- `{trisomy}_risk_level`: "High Risk" (>5%) or "Low Risk" (≤5%)

## Risk Classification Logic

- **High Risk**: Probability > 5% → Shows as ">1/20"
- **Low Risk**: Probability ≤ 5% → Shows as "1/X" format

## Features

1. **Automated Processing**: Processes all samples in batch
2. **Multiple Trisomies**: Calculates risks for T13, T18, and T21
3. **Clinical Format**: Results in clinically meaningful ratios
4. **Summary Reports**: Optional detailed analysis reports
5. **Error Handling**: Robust handling of missing data

## Command Line Options

```
python3 nipt_risk_calculator.py [-h] [--output OUTPUT] [--report] [--verbose] input_file

positional arguments:
  input_file            Input TSV file with z-scores

optional arguments:
  -h, --help            show this help message and exit
  --output OUTPUT, -o OUTPUT
                        Output CSV file (optional)
  --report, -r          Generate summary report
  --verbose, -v         Verbose output
```

## Example Output

```csv
sample,chr21,chr18,chr13,t21_probability_pct,t21_ratio,t21_risk_level
Sample1,-0.067,-3.08,-0.22,0.0,"1/461,222",Low Risk
Sample2,-1.003,-2.06,-0.82,0.0,"1/2,994,604",Low Risk
```

## Dependencies

- Python 3.6+
- pandas
- numpy

Install dependencies:
```bash
pip install pandas numpy
```
