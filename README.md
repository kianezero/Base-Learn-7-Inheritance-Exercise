# Base-Learn-7-Inheritance-Exercise

# Input Parameter
```
1. Deploy Salesperson:
Parameter	Value
_IDNUMBER	55555
_MANAGERID	12345
_HOURLYRATE	20
2. Deploy EngineeringManager:
Parameter	Value
_IDNUMBER	54321
_MANAGERID	11111
_ANNUALSALARY	200000
3. Deploy InheritanceSubmission:
Parameter	Value
_SALESPERSON	[Alamat Contract Salesperson]
_ENGINEERINGMANAGER	[Alamat EngineeringManager]
```

# Submit Contract Here

>> https://docs.base.org/learn/inheritance/inheritance-exercise

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// Abstract base contract
abstract contract Employee {
    uint public idNumber;
    uint public managerId;
    
    constructor(uint _idNumber, uint _managerId) {
        idNumber = _idNumber;
        managerId = _managerId;
    }
    
    function getAnnualCost() public view virtual returns (uint);
}

// Salaried employee contract
contract Salaried is Employee {
    uint public annualSalary;
    
    constructor(uint _idNumber, uint _managerId, uint _annualSalary) 
        Employee(_idNumber, _managerId) {
        annualSalary = _annualSalary;
    }
    
    function getAnnualCost() public view override returns (uint) {
        return annualSalary;
    }
}

// Hourly employee contract
contract Hourly is Employee {
    uint public hourlyRate;
    
    constructor(uint _idNumber, uint _managerId, uint _hourlyRate) 
        Employee(_idNumber, _managerId) {
        hourlyRate = _hourlyRate;
    }
    
    function getAnnualCost() public view override returns (uint) {
        return hourlyRate * 2080; // 2080 hours per year
    }
}

// Manager contract
contract Manager {
    uint[] public employeeIds;
    
    function addReport(uint _employeeId) public {
        employeeIds.push(_employeeId);
    }
    
    function resetReports() public {
        delete employeeIds;
    }
    
    function getEmployeeIds() public view returns (uint[] memory) {
        return employeeIds;
    }
}

// Salesperson contract (inherits from Hourly)
contract Salesperson is Hourly {
    constructor(uint _idNumber, uint _managerId, uint _hourlyRate) 
        Hourly(_idNumber, _managerId, _hourlyRate) {
    }
}

// Engineering Manager contract (multiple inheritance)
contract EngineeringManager is Salaried, Manager {
    constructor(uint _idNumber, uint _managerId, uint _annualSalary) 
        Salaried(_idNumber, _managerId, _annualSalary) {
    }
}

// Submission contract
contract InheritanceSubmission {
    address public salesPerson;
    address public engineeringManager;

    constructor(address _salesPerson, address _engineeringManager) {
        salesPerson = _salesPerson;
        engineeringManager = _engineeringManager;
    }
}
```
