

pragma solidity >=0.5.0 <0.9.0;  

contract escro{
    
    address agent;
    mapping (address => uint256) public deposit;
    
    modifier onlyagent(){
        require(msg.sender == agent);
        _;
    }
    
    constructor () public{
        agent = msg.sender;
    } 
    
    function deposits (address payee) public onlyagent payable{
        uint256 amount = msg.value;
        deposit[payee] = deposit[payee] + amount;
    }
    
    function withdraw(address payable payee) public onlyagent{
        uint256 payment = deposit[payee];
        deposit[payee] = 0;
        payee.transfer(payment);
    }
} 