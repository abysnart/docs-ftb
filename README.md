### API Endpoints

#### User
GET `/user/nonce/:walletAddress`

- call when connect wallet to get nonce for signing.

POST `/user/login`
- request: `{ walletAddress: string, sign: string }`
- response: `{ accessToken: string }`

GET `/user/balances`
- get user token balances.
- header: `Authorization: accessToken`
- response: `{ token: number }`

#### PVE

GET `/pve/formation`
- get lasted formation of PVE team.
- header: `Authorization: accessToken`
- response: `{ power: number, team: IPlayer[], arrange: number[] }`
- interfaces: 
```
IPlayer
{
	tokenId: number;
    name: string;
    image: string;
    nation: string;
    club: {
        image: string;
        name: string;
    };
    rating: number;
    type: string;
    rank: "normal" | "professional" | "expert" | "super star";
    attributes: {
        atk: number;
        def: number;
        str: number;
        stm: number;
        ski: number;
    };
}
```

PATCH `/pve/formation`
- update formation of PVE team.
- header: `Authorization: accessToken`
- request: `{ team: number[], arrange: number[] }`
- example: 
```
{
    team: [1,2,3,4,5], // array of NFT tokenID
    arrange: [4,4,2], // 4-4-2 formation
}
```

POST `/pve/start`
- start a PVE match
- header: `Authorization: accessToken`
- request: `{ token: number }`
- response:
```
{
    enemyPower: 1234, // Power of enemy team
    enemyTeam: {
    	team: IPlayer[],
    	arrange: [4,4,2]
    }
    result: {
    	win: boolean,
        tokenBonus: number,
 		tokenLoss: number
    }
}
```

#### NFT

GET `/nft/list`
- get list of user nfts
- header: `Authorization: accessToken`
- response: `IPlayer[]`


PATCH `/nft/level/up`
- up level of NFT
- header: `Authorization: accessToken`
- request: `{ tokenId: number }`
- response: `IPlayer[]`

GET `/nft/level/cost`
- up cost for up level of NFT
