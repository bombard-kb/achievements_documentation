# Achievements

## Definition
Achievement is an external property of the token, hence it can't be removed from the token, it can't be sold or transfered separately from the token.

## Achievements vs Trophies
Trophies on the other hand are another ERC721 token, which is associated with the original token or the ETH address of the owner and can be transfered and sold separately.

## Proposed Interface for Achievements

```
interface Achievements {
  /// This event is fired when an achievement is added to a token
  event Achievement(uint256 _tokenId, uint256 _achievementId);
  
  /// This is the function to add achievements to the token, can be called only by the owner of the contract
  function addAchievement(uint256 _tokenId, uint256 _achievementId) external;
  
  /// This is the function to get a list of achievment ids for a token
  function listOfAchievements(uint _tokenId) external returns (uint256[]);
  
  /// This is the function to get the metadata for the achievement:
  /// @title - short description of the achievement
  /// @description - detailed description of the achievement
  /// @icon - IPFS hash to get the icon image of the achievement, should be SVG(?)
  function achievement(uint _achievementId) returns (string title, string desciption, string icon);
}
```
