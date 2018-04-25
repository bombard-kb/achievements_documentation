# Achievements

## Definition
Achievement is an external property of the token, hence it can't be removed from the token, it can't be sold or transfered separately from the token.

## Achievements vs Trophies
Trophies on the other hand are another ERC721 tokens, which are associated with the original token or the ETH address of the owner and can be transfered and sold separately.

## Proposed Interface for Achievements

```
interface Achievements {
  /// This event is fired when an achievement is added to a token
  event Achievement(uint256 _tokenId, uint256 _achievementId);
  
  /// This is the function to add an achievement to a token, can be called only by the owner of the contract
  function addAchievement(uint256 _tokenId, uint256 _achievementId) external;
  
  /// This is the function to get a list of achievment ids for a token
  function listOfAchievements(uint256 _tokenId) external returns (uint256[]);
  
  /// This is the function to get the metadata for the achievement:
  /// @title - short description of the achievement
  /// @description - detailed description of the achievement
  /// @icon - IPFS hash to get the icon image of the achievement, should be SVG(?)
  function achievement(uint256 _achievementId) returns (string title, string description, string icon);
}
```

## Proposed Scenario

### Given

- Player (P)
- ERC721 Contract (TC)
- ERC721 Token of TC (T)
- Off chain Game (G)
- Achievements Contract (AC)
- Achievement Token of AC (AT)

### Relationships

- P owns T
- P plays G using T
- G owns AC and creates AT
- T owns AT

### Scenario

When P has made a significant achievement, G creates a transaction to `addAchievement` on AC, creating AT, which represents the achievement.

P has no direct control of the AT, but can buy, sell or transfer T, which owns AT.

Owner of TC, building the UI to represent the properties of T can use infromation about AT to visualize achievements T owns.
