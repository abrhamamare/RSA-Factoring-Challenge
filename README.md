# RSA Factoring Challenge

Educational Bash scripts for exploring **integer factorization**, a mathematical problem relevant to RSA cryptography. This repository contains two executable scripts, `factors` and `rsa`. **Both currently use the same general-purpose factorization procedure**; the name `rsa` does not mean it implements RSA encryption or a specialized attack on realistic RSA keys.

## Requirements

- Bash
- GNU coreutils `factor` and `tr`
- `bc` for integer multiplication and comparison
- A Unix-like shell environment with these commands on `PATH`

## Usage

Clone the repository and make the scripts executable:

```bash
git clone https://github.com/abrhamamare/RSA-Factoring-Challenge.git
cd RSA-Factoring-Challenge
chmod +x factors rsa
```

Create a plain-text input file containing **one positive integer per line**:

```bash
printf '15\n21\n' > numbers.txt
./factors numbers.txt
./rsa numbers.txt
```

For these examples, each script should print lines of the form `15=5*3` and `21=7*3` (factor order may vary). The scripts call the system `factor` utility for each line, then print the first factor and the product of the remaining factors, placing the larger of those two quantities first.

## How the scripts work

1. Accept exactly one argument: a path to the input file.
2. Read the file line by line using a Bash `while read` loop.
3. Call `factor` on each input number to obtain its prime factors.
4. If there are more than two prime factors, multiply all but the first using `bc`.
5. Compare the resulting two quantities using `bc`, then print `number=larger*smaller`.

For example, `12 = 2 × 2 × 3` may be represented as `12=6*2`. The output therefore gives a **two-factor decomposition**, not necessarily two prime factors. The scripts do not check that an input is a semiprime.

## Mathematical background

RSA uses a modulus `n = p × q`, where `p` and `q` are large primes. Knowledge of the factors can allow an attacker to derive private-key material when other RSA parameters are known. The challenge here illustrates factorization with small, educational examples; it does not generate RSA keys, recover private keys, or decrypt messages.

## Limitations and security notes

- **Not suitable for real-world RSA key breaking.** Factorization of properly generated, modern RSA moduli is computationally infeasible with this approach.
- The scripts depend on the external `factor` utility, not a custom factorization algorithm.
- Input is not rigorously validated. Blank lines, non-integers, missing files, and unexpected command output can cause errors or misleading results.
- Unquoted variable expansions and basic `read` handling mean unusual input is not robustly supported.
- The `rsa` script currently duplicates the behavior of `factors`; it does not enforce an RSA-semiprime-only constraint.
- There are no automated tests in the current repository.

## Potential improvements

- Validate numeric input and file existence, and quote shell expansions.
- Add tests for primes, semiprimes, composite numbers with repeated factors, malformed input, and large values.
- Consolidate duplicate code and distinguish general factorization from semiprime-specific validation.
- Benchmark performance and explain its practical limits.

## Educational purpose

This project is for learning number theory, Bash scripting, and the role of integer factorization in public-key cryptography. It is **not** a security assessment tool.
