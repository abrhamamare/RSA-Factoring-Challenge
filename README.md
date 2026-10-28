# RSA Factoring Challenge

A Bash scripting exercise that reads integers from a text file and prints a factorization for each input using the system's `factor` utility.

## What is in this repository?

- `factors` — reads input numbers and formats factors reported by `factor`.
- `rsa` — a related challenge script with the same underlying approach.

**Scope:** These scripts are learning exercises. They rely on the external `factor` command and do **not** implement an independent integer-factorization algorithm or demonstrate the ability to break real-world RSA keys.

## Requirements

- Bash
- GNU coreutils `factor`
- `bc` calculator
- `tr`

## Usage

Create a plain-text file containing one positive integer per line:

```text
15
21
77
```

Then run:

```bash
chmod +x factors rsa
./factors numbers.txt
./rsa numbers.txt
```

The scripts call `factor` and format the results. For example, the factors of 15 are 3 and 5. The scripts' exact formatting and behavior should be verified before relying on their output.

## Cryptography context

RSA security depends partly on the difficulty of factoring the product of two sufficiently large secret primes. Small classroom examples can be factored easily; production RSA moduli are vastly larger. This project is intended to illustrate integer factorization and shell scripting, not cryptanalysis of production RSA.

## Known limitations

- Input validation and error handling are minimal.
- The scripts depend on GNU `factor`, so portability is limited.
- Factorization of large inputs may be slow or infeasible.
- There is no automated test suite yet.

## Planned improvements

- Validate file paths and numeric input.
- Handle blank lines and malformed input.
- Add tests for prime, composite, and invalid values.
- Document expected output and failure behavior.

## Responsible use

Use this code for learning and authorized experiments only.
