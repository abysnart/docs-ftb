### API Endpoints

#### Market
GET `/market/orders`
- get order list for homepage
- response: `IOrderCreatedEvent && IPlayer`
```
IOrderCreatedEvent
{
    transactionHash: string,
    tokenId: number,
    orderId: number,
    createdTime: number,
    creator: string,
    targetPrice: number
}
```

GET `/market/history/:tokenId`
- get trading history for a tokenId
- response: `IOrderTakenEvent && IPlayer`
```
IOrderTakenEvent
{
    transactionHash: string,
    buyer: string,
    seller: string,
    totalPrice: number,
    orderId: number
}
```

POST `/user/login`
- request: `{ walletAddress: string, sign: string }`
- response: `{ accessToken: string }`

GET `/user/balances`
- get user token balances.
- header: `Authorization: accessToken`
- response: `{ token: number }`


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

POST `/user/withdrawal`
- withdraw token to wallet.
- header: `Authorization: accessToken`
- request: `{ amount: number }`
- response: `{ nonce: string, address: string, signature: string, amount: string }`

#### PVE

GET `/pve/season`
- get current season number and matches.
- header: `Authorization: accessToken`
- response: ` { number: number, match: number, total: number }`

GET `/pve/formation`
- get lasted formation of PVE team.
- header: `Authorization: accessToken`
- response: `{ team: IPlayer[], arrange: number[] }`
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
    level: number;
    exp: number;
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

GET `/nft/mint/:walletAddress`
- mint nft (DEV ONLY)
- response: `{}`

GET `/nft/list`
- get list of user nfts
- header: `Authorization: accessToken`
- response: `IPlayer[]`

GET `/nft/metadata/:tokenId`
- get metadata of NFT (for marketplace)
- response: `IMetadata`
```
IMetadata
{
    name: string;
    description: string;
    image: string;
    attributes: TAttributes;
}
```

PATCH `/nft/level/up/:tokenId`
- up level of NFT
- header: `Authorization: accessToken`
- response: `IPlayer`

GET `/nft/level/cost`
- up cost for up level of NFT
- response: `{ level: number, exp: number, token: number }`
