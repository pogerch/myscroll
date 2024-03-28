pragma solidity ^0.8.20;
contract Contract1 is ERC20, ERC20Burnable, ERC20Pausable, Ownable, ERC20Permit, ERC20Votes, ERC20FlashMint {
    constructor(address initialOwner)
        ERC20("contract1", "ctc")
        Ownable(initialOwner)
        ERC20Permit("contract1")
    {}

    function pause() public onlyOwner {
        _pause();
    }

    function unpause() public onlyOwner {
        _unpause();
    }

    function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }

    // The following functions are overrides required by Solidity.

    function _update(address from, address to, uint256 value)
        internal
        override(ERC20, ERC20Pausable, ERC20Votes)
    {
        super._update(from, to, value);
    }

    function nonces(address owner)
        public
        view
        override(ERC20Permit, Nonces)
        returns (uint256)
    {
        return super.nonces(owner);
    }
}
