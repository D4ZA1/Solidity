# 📘 Solidity Notes

Solidity is a high-level, statically-typed programming language for writing smart contracts on Ethereum and other blockchain platforms. Inspired by JavaScript, Python, and C++, Solidity is widely used for writing decentralized applications (dApps).

---

## 📌 1. Data Types in Solidity

Solidity supports both value and reference types.

### 🔹 Value Types

Value types store data directly and are copied when assigned or passed to functions.

| Type     | Description                          | Example                      |
|----------|--------------------------------------|------------------------------|
| `uint`   | Unsigned integer (0 and above)       | `uint age = 25;`             |
| `int`    | Signed integer (positive or negative)| `int temp = -10;`            |
| `bool`   | Boolean value                        | `bool isActive = true;`      |
| `address`| Ethereum address (20-byte)           | `address user = msg.sender;`|
| `bytes1` to `bytes32` | Fixed-size byte arrays | `bytes1 flag = 0x01;`        |

- `uint` is an alias for `uint256`
- Other common forms: `uint8`, `uint16`, ..., `uint256`

---

### 🔹 Reference Types

Reference types store locations pointing to the actual data.

- `string`: UTF-8 encoded dynamic text  
  Example: `string name = "Alice";`

- `bytes`: Dynamic-size byte array  
  Example: `bytes data = "0x1234";`

- `arrays`: Collections of values of the same type

- `structs`: User-defined types

- `mapping`: Key-value storage

---

## 📌 2. Variables in Solidity

Solidity has different kinds of variables with distinct scopes.

### 🔹 Types of Variables

| Type             | Scope               | Description                             |
|------------------|---------------------|-----------------------------------------|
| **State**        | Global (Contract)   | Declared outside functions. Stored on blockchain. |
| **Local**        | Inside functions    | Temporary, not stored on blockchain.    |
| **Global (Built-in)** | Auto-available | Predefined variables like `msg.sender`  |

---

### 🔹 Visibility Modifiers

- `public`: Accessible from anywhere
- `private`: Accessible only within the contract
- `internal`: Accessible in current and derived contracts
- `external`: Only accessible from outside the contract

### 🔹 Example

```solidity
pragma solidity ^0.8.0;

contract VariableExample {
    uint public count = 0;  // State variable

    function increment() public {
        uint temp = 5;      // Local variable
        count += temp;
    }
}
```

📌 3. Arrays in Solidity

Arrays store multiple items of the same type.
🔹 Fixed-size Array

uint[3] fixedArray = [1, 2, 3];

🔹 Dynamic-size Array

uint[] public dynamicArray;

function addElement(uint value) public {
    dynamicArray.push(value);
}

🔹 Common Array Functions
Function	Description
push(value)	Adds an element to the end
pop()	Removes the last element
length	Returns the number of elements
delete arr[i]	Resets the value at index i to default
🔹 Example
```solidity
pragma solidity ^0.8.0;

contract ArrayExample {
    uint[] public numbers;

    function add(uint num) public {
        numbers.push(num);
    }

    function get(uint index) public view returns (uint) {
        return numbers[index];
    }
}
```
📌 4. Functions in Solidity

Functions are reusable blocks of code that perform actions.
🔹 Syntax

function functionName([parameters]) [visibility] [modifiers] [returns(returnType)] {
    // logic
}

🔹 Visibility
Visibility	Description
public	Accessible internally and externally
private	Accessible only within the declaring contract
internal	Accessible in the contract and derived contracts
external	Callable only from external accounts or contracts
🔹 Function Modifiers

    view: Does not modify the contract state

    pure: Does not read or modify contract state

    payable: Function can receive Ether

🔹 Public Function Example

pragma solidity ^0.8.0;

contract Math {
    function add(uint a, uint b) public pure returns (uint) {
        return a + b;
    }
}

🔹 Private Function Example
```solidity
pragma solidity ^0.8.0;

contract SecretMath {
    function _internalAdd(uint a, uint b) private pure returns (uint) {
        return a + b;
    }

    function callPrivate() public pure returns (uint) {
        return _internalAdd(5, 3);
    }
}
```
