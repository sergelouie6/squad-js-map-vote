## MapVote
The `MapVote` plugin for squad js based on the original version https://github.com/maskedmonkyman/squad-js-map-vote

### Commands

#### User Commands
- `!vote help` - sends possbile commands to a player in the from of a warning
- `!vote choices` - sends choices to player in the from of a warning
- `!vote results` - sends player the results in a warning

#### Admin Commands
- `!vote start` - Starts a vote with 6 layers, random modes
- `!vote cancel` - Cancels current round of voting
- `!vote cancelauto` - Cancel scheduled automatic start of vote
- `!vote end` - Gently ends the current vote and announces the winner layer
- `!vote restart` - Restarts voting with 6 random maps and modes
- `!vote broadcast` - Broadcasts current voting results - happens every 7m automatically

##### Vote by modes
- `!vote start *_raas` - Starts a vote with 6 layers, all RAAS
- `!vote start *_aas` - Starts a vote with 6 layers, all AAS
- `!vote start *_inv` - Starts a vote with 6 layers, all INV

##### Vote by map
- `!vote start yeh gor lash gor albas` - Starts a vote with X maps, random modes

##### Vote by map + mode, mixed
- `!vote start yeh_raas gor_raas lash_inv gor albas_inv` - Starts a vote with X maps, X modes


### Options
#### commandPrefix
###### Description
The command name to use in chat.
###### Default
```
!vote
```
#### automaticVoteStart
###### Description
A map vote will automatically start after a new match if set to true.
###### Default
```json
true
```
#### votingDuration
###### Description
How long the voting will be active (in minutes). Set to 0 for unlimited time.
###### Default
```json
0
```
#### minPlayersForVote
###### Description
The number of players needed on the server for a vote to start.
###### Default
```json
40
```
#### voteWaitTimeFromMatchStart
###### Description
The time in mins from the start of a round to the start of a new map vote.
###### Default
```json
15
```
#### voteBroadcastInterval
###### Description
The broadcast interval for vote notification in mins.
###### Default
```json
7
```
#### automaticSeedingMode
###### Description
Instantly change to a seeding layer if server has less than 5 players and set next layer to a seeding layer if server has less than 20 players.
###### Default
```json
true
```
#### numberRecentMapsToExlude
###### Description
The random layer list will not include the X recent maps
###### Default
```json
4
```
#### gamemodeWhitelist
###### Description
The random layer list will be generated with only selected gamemodes.
###### Default
```json
[ "AAS", "RAAS", "INVASION" ]
```
#### layerFilteringMode
###### Description
Select Whitelist mode or Blacklist mode.
###### Default
```json
"blacklist"
```
#### layerLevelWhitelist
###### Description
The random layer list will include ONLY the whitelisted layers or levels. (acceptable formats: Gorodok/Gorodok_RAAS/Gorodok_AAS_v1).
###### Default
```
[]
```
#### layerLevelBlacklist
###### Description
The random layer list will NOT include the blacklisted layers or levels. (acceptable formats: Gorodok/Gorodok_RAAS/Gorodok_AAS_v1).
###### Default
```
[]
```
#### applyBlacklistToWhitelist
###### Description
If set to true the blacklisted layers will be filtered out also in whitelist mode.
###### Default
```json
true
```
#### minRaasEntries
###### Description
Minimum amount of RAAS layers in the vote list.
###### Default
```json
2
```
#### hideVotesCount
###### Description
Hides the number of votes a layer received in broadcast message.
###### Default
```json
false
```
#### showRerollOption
###### Description
vote option to restart the vote with random entries.
###### Default
```json
false
```
#### voteBroadcastMessage
###### Description
Message that is sent as broadcast to announce a vote.
###### Default
```json
"✯ MAPVOTE ✯\nVote for the next map by writing in chat the corresponding number!"
```
#### voteWinnerBroadcastMessage
###### Description
Message that is sent as broadcast to announce the winning layer.
###### Default
```json
"✯ MAPVOTE ✯\nThe winning layer is\n\n"
```
#### allowedSameMapEntries
###### Description
Allowed max NUMBER of times a map could appear in the vote list.
###### Default
```json
1
```
#### logToDiscord
###### Description
Enables/disables vote logging to Discord.
###### Default
```json
false
```
#### channelID
###### Description
The ID of the channel to log votes to.
###### Default
```json
"112233445566778899"
```
#### timezone
###### Description
Timezone relative to UTC time. 0 for UTC, 2 for CEST (UTC+2), -1 (UTC-1) 
###### Default
```json
0
```
#### timeFrames
###### Description
Array of timeframes that allows to override options based on local time. See example configuration
###### Default
```json
[]
```
###### Timeframe format
```javascript
{
    name: "friendly name", // a friendly name visible in the logs
    start: "12:00", // timeframe start time <hour>:<minutes>
    end: "18:00", // timeframe end time <hour>:<minutes>
    overrides: { // options to override
        automaticVoteStart: false,
        layerLevelBlacklist: [ "Anvil", "Chora" ]
    }
}
```
### Example configuration
```json
{
    "plugin": "MapVote",
    "enabled": true,
    "discordClient": "discord",
    "automaticVoteStart": true,
    "votingDuration": 0,
    "minPlayersForVote": 30,
    "voteWaitTimeFromMatchStart": 10,
    "voteBroadcastInterval": 7,
    "numberRecentMapsToExlude": 4,
    "automaticSeedingMode": true,
    "gamemodeWhitelist": [ "AAS", "RAAS", "Invasion" ],
    "layerLevelBlacklist": [ "BlackCoast_Seed" ],
    "layerLevelWhitelist": [ "Yeho", "Gorodok", "Mutaha", "Narva", "Tallil" ],
    "applyBlacklistToWhitelist": true,
    "minRaasEntries": 2,
    "hideVotesCount": false,
    "showRerollOption": false,
    "voteBroadcastMessage": "✯ MAPVOTE ✯\nVote for the next map by writing in chat the corresponding number!",
    "voteWinnerBroadcastMessage": "✯ MAPVOTE ✯\nThe winning layer is\n\n",
    "allowedSameMapEntries": 1,
    "logToDiscord": true,
    "channelID": "112233445566778899",
    "timezone": 2,
    "timeFrames": [
        {
            "name": "follow layer rotation list",
            "start": "12:00",
            "end": "18:00",
            "overrides": {
                "automaticVoteStart": false
            }
        },
        {
            "start": "22:00",
            "end": "02:00",
            "overrides": {
                "voteBroadcastMessage": "Late night games? Vote your favourite map!"
            }
        }
    ]
}
```
