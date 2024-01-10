# eBurger - Template Based Smart Contracts Static Analysis

<img src="static/eburger.png?raw=true" alt="eBurger" width="600"/>

eBurger is a way to quickly interact with solidity smart contracts.

Running scanners won't win you competitions. spin up custom templates tailored to specific projects in minutes ([Wiki](https://github.com/forefy/eburger/wiki)).

- [Comparison table](#comparison-table)
- [How to install](#how-to-install)
- [How to run](#how-to-run)
    - [Usage demo](#usage-demo)
    - [How to run simply](#how-to-run-simply)
    - [How to run - advanced](#how-to-run---advanced)
- [Adding templates](#adding-templates)
- [What is missing](#what-is-missing)


## Comparison table
| Active Static Analyzer                                 | Language        | Visualization Graph    | 2 Minutes to write a custom template with Chat GPT    | Many findings that are already found before the contest began | Would want to eat |
|--------------------------------------------------------|-----------------|------------------------|-------------------------------------------------------|---------------------------------------------------------------|-------------------|
| [eBurger](https://github.com/forefy/eburger)           | Python          | ✅                     | ✅                                                    |                                                               | ✅                |
| [Slither](https://github.com/crytic/slither)           | Python          | ✅                     |                                                       | ✅                                                            |                   |
| [4naly3er](https://github.com/Picodes/4naly3er)        | TypeScript 🤮   |                        |                                                       | ✅                                                            |                   |
| [mythril](https://github.com/Consensys/mythril)        | Python          |                        |                                                       | ✅                                                            |                   |

Forgot one? open an issue :)

## How to install
```
git clone https://github.com/forefy/eburger.git
pip3 install .
eburger -h
```

## How to run

### Usage demo
<figure class="video_container">
    <video controls="true" allowfullscreen="true">
        <source src="./static/eburger.mp4" type="video/mp4">
    </video>
</figure>

### Simple examples
Simplest:
```bash
cd MyProject/
eburger
cat eburger-results.json
```
..

This will run a focused scan on one file and it's dependencies:
```
eburger -f ../ProjectToScan/src/SomeContract.sol
```
..

This will compile the solidity files inside ProjectToScan, as well as specifying remappings configured in the project.
```
eburger -f ../ProjectToScan/src/ -r @openzeppelin/=../ProjectToScan/lib/openzeppelin-contracts/
```


### Advanced usage
Refer to the [Wiki](https://github.com/forefy/eburger/wiki/Advanced-usage).


## Adding templates
Templates can be added by adding new YAML files under the `templates/` directory.

If you are using eburger as a python package (installed with pip install), the templates location can be found with running `pip3 show eburger` or by running the tool on a contract and seeing the templates path printed to the console.

For documentation refer to the [Wiki](https://github.com/forefy/eburger/wiki/Templates).


## How it looks like
Here's an example
```bash
cd MyProject/
eburger
cat eburger-results.json
```
```json
{
    "name": "tx.origin Used for Access Control",
    "description": "Imagine a user with an authorized address interacts with a malicious contract. This malicious contract then calls your contract that uses tx.origin for authentication. Since tx.origin will refer to the user's address (the original sender of the transaction), the malicious contract might gain unauthorized access.",
    "severity": "Low",
    "results": [
        {
            "file": "vulnerable_contracts/tx_origin_used_for_access_control.sol",
            "lines": "Line 11 Columns 8-62",
            "code": "require(tx.origin == owner, 'Caller is not the owner')"
        }
    ]
}
```

Above command will also generate an AST, pythonified AST and a visual call flow graph under the folder `.eburger`.

Here's an example of the interactive graph
![eBurger](static/network_graph.png?raw=true "eBurger Network Graph")


## Features
- YAML template support to query contract structure and raise insights for any matches
- Foundry support ❣️
- Call Flow Graph inspired by naming conventions of Solidity
- Search specific segments and highlight by parameter, function, contract etc
- Extensive control on graph layout
- View only the code related to the contract and not all the libraries in the world
- Community and free support via [Discord](discord.gg/WaVMpBtxdB)


## What is missing
As you can see, the tool is still in the making - what features would you like to see? let us know!