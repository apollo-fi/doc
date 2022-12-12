[TOC]

# 0. Summary

## Environment
* dev: **http://api.apollopro.xyz**

## APIs Overview

| link                               | url                                | description                                       |   status   | modify date |
|------------------------------------|------------------------------------|---------------------------------------------------|:----------:|:-----------:|
| [1.1 LoginMessage](#1-1)           | GET /api/v1/login/message          | Get the login string to be signed                 | completed  |             |
| [1.2 Login](#1-2)                  | POST /api/v1/login                 | Login                                             | completed  |             |
| [2.1 GetUser](#2-1)                | GET /api/v1/user/{address}         | Get user info                                     | completed  |             |
| [2.2 CheckUsername](#2-2)          | GET /api/v1/user/checkUsername     | Check if username is already used                 | completed  |             |
| [2.3 UpdateUser](#2-3)             | PUT /api/v1/user                   | Update user info                                  | completed  |             |
| [2.4 GetUserFollowing](#2-4)       | GET /api/v1/user/following         | Get user watchlist                                | completed  |             |
| [2.5 GetUserFollower](#2-5)        | GET /api/v1/user/follower          | Get user fan list                                 | completed  |             |
| [2.6 FollowOrUnFollow](#2-6)       | POST /api/v1/user/follow           | Follow/Unfollow                                   | completed  |             |
| [2.7 GetUserActivity](#2-7)        | GET /api/v1/user/activity          | Paging to get the list of user activity           | completed  |             |
| [2.8 FavoriteOrUnFavorite](#2-8)   | POST /api/v1/user/favorite         | Favorite/UnFavorite                               | completed  | 2022.11.29  |
| [2.9 GetCollect](#2-9)             | GET /api/v1/user/collect           | Paging to get the list of user collect            | completed  | 2022.12.06  |
| [2.10 GetFavorite](#2-10)          | GET /api/v1/user/favorite          | Paging to get the list of user favorite           | completed  | 2022.12.06  |
| [2.11 UploadPreSignUrl](#2-11)     | POST /api/v1/user/uploadPreSignUrl | Get oss presigned url                             | completed  | 2022.12.08  |
| [2.12 UploadCredential](#2-12)     | POST /api/v1/user/uploadCredential | Get oss tmp credential                            | completed  | 2022.12.08  |
| [3.1 GetCollectionRanking](#3-1)   | GET /api/v1/ranking/collection     | Paging to get the list of collection ranking      | completed  |             |
| [3.2 GetCollectionTrending](#3-2)  | GET /api/v1/trending/collection    | Paging to get the list of collection trending     | completed  | 2022.11.25  |
| [4.1 Search](#4-1)                 | GET /api/v1/search                 | search collection/nft/user                        | completed  | 2022.11.25  |
| [4.2 GetCollectionByAddress](#4-2) | GET /api/v1/collection/{address}   | Get collection detail                             | completed  | 2022.11.25  |
| [4.3 GetCollectionActivity](#4-3)  | GET /api/v1/activity               | Paging to get the list of collection/nft activity | completed  | 2022.11.25  |
| [4.4 SearchNft](#4-4)              | GET /api/v1/nfts                   | Search nfts                                       | completed  | 2022.11.25  |
| [4.5 GetNftByTokenId](#4-5)        | GET /api/v1/nft                    | Get nft detail                                    | completed  | 2022.11.25  |
| [4.6 GetNftCondition](#4-6)        | GET /api/v1/nftCondition           | Get condition                                     | completed  | 2022.11.25  |
| [4.7 GetCollectionCondition](#4-7) | GET /api/v1/collectionCondition    | Get condition of collection                       | completed  | 2022.11.25  |
| [4.8 GetMoreNft](#4-8)             | GET /api/v1/moreNft                | Get more nft                                      | completed  | 2022.12.02  |
| [5.1 GetNFTPopular](#5-1)          | GET /api/v1/nft/popular            |                                                   | processing |             |
| [6.1 GetOrder](#6-1)               | GET /api/v1/order                  | Paging to get the list of order                   | completed  |             |
| [6.2 Listing](#6-2)                | POST /api/v1/order/listing         | listing                                           | completed  |             |
| [6.3 Offer](#6-3)                  | POST /api/v1/order/offer           | offer                                             | completed  |             |
| [6.4 CreateBnpl](#6-4)             | POST /api/v1/order/bnpl            | create bnpl order                                 | completed  |             |

## Error Code

| code   | description                                             |
|--------|---------------------------------------------------------|
| 200    | success                                                 |
| 400    | parameters error                                        |
| 403001 | token invalid                                           |
| 403002 | illegal access                                          |
| 403003 | token expired                                           |
| 500    | fail                                                    |
| 500001 | record not exists                                       |
| 500002 | record update failed                                    |
| 500101 | signature invalid                                       |
| 500201 | all currency tokens in the order must be the same token |
| 500202 | invalid counter                                         |
| 500203 | order already cancelled                                 |
| 500204 | order already filled                                    |
| 500205 | insufficient approvals                                  |
| 500206 | order already exists                                    |
| 500207 | order signature invalid                                 |
| 500208 | order already broken                                    |
| 500209 | order invalid price                                     |

# 1. Login APIs

## <a id="1-1">1.1 LoginMessage</a>

### 1.1.1 URL

```
GET /api/v1/login/message?address=0x96216849c49358B10257cb55b28eA603c874b05E
```

### 1.1.2 Request

#### 1.1.2.1 header

```
Content-Type: application/json
```

#### 1.1.2.2 body

```

```

### 1.1.3 response

```
{
  "code": 200,
  "msg": "success",
  "data": {
    "message": "Please sign this message to log in.\nThis request will not trigger a blockchain transaction or cost any gas fees.\n\nBy signing, you accept Apollo's Terms of Service, which you can find here: terms-of-service-link\nWallet address:\n0x0000000000000000000000000000000000000000\nNonce:\ndef0102d-45ae-4c5b-babe-45df0d392dd6"
  }
}
```

## <a id="1-2">1.2 Login</a>

### 1.2.1 URL

```
POST /api/v1/login
```

### 1.2.2 Request

#### 1.2.2.1 header

```
Content-Type: application/json
```

#### 1.2.2.2 body

```
{
  "address": "0x0000000000000000000000000000000000000000",
  "message": "Please sign this message to log in.\nThis request will not trigger a blockchain transaction or cost any gas fees.\n\nBy signing, you accept Apollo's Terms of Service, which you can find here: terms-of-service-link\nWallet address:\n0x0000000000000000000000000000000000000000\nNonce:\ndef0102d-45ae-4c5b-babe-45df0d392dd6",
  "signature": "0x6b4114df3df8c3c236d2a27c9cc7486065d750cf1c1a0635cb0ee8cd56aab42703cb46de2e1ec798c5f3b9e85be116db7771561bac12864fa0784b36372e9e511b"
}
```

### 1.2.3 response

```
{
  "code": 200,
  "msg": "success",
  "data": {
    "user": {
      "id": 4,
      "createTime": "2022-09-29T01:52:34.696Z",
      "updateTime": "2022-09-29T01:52:34.696Z",
      "address": ":0x70e6821f674BeFB152F1b2ad7017EE89Eb55E222",
      "name": ":0x70e6821f674BeFB152F1b2ad7017EE89Eb55E222",
      "headImageUrl": "",
      "backgroundUrl": ""
    },
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJJZCI6NCwiQWRkcmVzcyI6IjB4OTYyMTY4NDljNDkzNThCMTAyNTdjYjU1YjI4ZUE2MDNjODc0YjA1RSIsIlVzZXJuYW1lIjoiMHg5NjIxNjg0OWM0OTM1OEIxMDI1N2NiNTViMjhlQTYwM2M4NzRiMDVFIiwiQnVmZmVyVGltZSI6ODY0MDAwMDAwMDAwMDAsImlzcyI6ImFwb2xsby1maSIsImV4cCI6MTY2NTgxMTM4MSwibmJmIjoxNjY1MjA1NTgxfQ.NdYgSb1pXOpi7WPHS-tQNc3hleTwgReC6_2dqYpq6SQ",
    "expiresAt": 1665811381932
  }
}
```

### 1.2.4 Remark

The signature method used by the front end
```
web3.eth.personal.sign
```

# 2. User APIs

## <a id="2-1">2.1 GetUser</a>

### 2.1.1 URL

```
GET /api/v1/user/{address}
```

### 2.1.2 Request

#### 2.1.2.1 header

```
Content-Type: application/json
```

#### 2.1.2.2 body

```
```

### 2.1.3 response

```
{
  "code": 200,
  "msg": "success",
  "data": {
    "id": 1,
    "address": "0x0000000000000000000000000000000000000000",
    "name: "0xaddress",
    "headImageUrl": "https://image.com/headImageUrl",
    "backgroundUrl": "https://image.com/backgroundUrl",
    "createTime": "2022-06-21 05:16:27",
    "tags": [
      {
        "name": "Gold Seller",
        "iconUrl: "https://image.com/iconUrl",
        "createTime": "2022-09-26 15:56:11"  // When the user got the tag
      },
      {
        "name": "Insight Man",
        "iconUrl: "https://image.com/iconUrl",
        "createTime": "2022-09-21 05:16:27"
      }
    ],
    "following": 10,
    "follower": 3
  }
}
```

## <a id="2-2">2.2 CheckUsername</a>

### 2.2.1 URL

```
GET /api/v1/user/checkUsername?name=test1
```

### 2.2.2 Request

#### 2.2.2.1 header

```
Content-Type: application/json
Authorization: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZGRyZXNzIjoiMHg1MjcyNzhBNzUwQTEzZEQ0MTU4QkNCMzFjNWZhODIzYjgxRjYwNERmIiwibmFtZSI6bnVsbCwiaWF0IjoxNjY0MTgzMjU1LCJleHAiOjE2NjQyNjk2NTUsImlzcyI6Ikxvb2tzIFJhcmUifQ.Azw362qxOZwW3HMkWHpEKvwrtuc7EF-Fmm4NIalUksE"
```

#### 2.2.2.2 body

```
```

### 2.2.3 response

```
{
  "code": 200,
  "msg": "success",
  "data": true  // true means it has been used
}
```

## <a id="2-3">2.3 UpdateUser</a>

### 2.3.1 URL

```
PUT /api/v1/user
```

### 2.3.2 Request

#### 2.3.2.1 header

```
Content-Type: application/json
Authorization: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZGRyZXNzIjoiMHg1MjcyNzhBNzUwQTEzZEQ0MTU4QkNCMzFjNWZhODIzYjgxRjYwNERmIiwibmFtZSI6bnVsbCwiaWF0IjoxNjY0MTgzMjU1LCJleHAiOjE2NjQyNjk2NTUsImlzcyI6Ikxvb2tzIFJhcmUifQ.Azw362qxOZwW3HMkWHpEKvwrtuc7EF-Fmm4NIalUksE"
```

#### 2.3.2.2 body

```
{
  "name": "0xaddress",
  "headImage": "aws s3 url",
  "backgroundImage": "aws s3 url"
}
```

### 2.3.3 response

```
{
  "code": 200,
  "msg": "success",
  "data": {
    "id": 4,
    "createBy": "",
    "updateBy": "",
    "createTime": "2022-09-29T01:52:34.696Z",
    "updateTime": "2022-10-08T07:33:59.851Z",
    "address": ":0x70e6821f674BeFB152F1b2ad7017EE89Eb55E222",
    "name": "test1",
    "headImageId": 30,
    "headImageUrl": "uploads/file/4b9169eb3e07e0e885eb62f7bfc41a33_20221008153359.png",
    "backgroundId": 31,
    "backgroundUrl": "uploads/file/f8d2e1584059489f8ffa3663b3223df2_20221008153359.png",
    "tags": [],
    "following": 1,
    "follower": 2
  }
}
```

## <a id="2-4">2.4 GetUserFollowing</a>

### 2.4.1 URL

```
GET /api/v1/user/following?page=1&pageSize=100&address=0x96216849c49358B10257cb55b28eA603c874b05E
```

### 2.4.2 Request

#### 2.4.2.1 header

```
Content-Type: application/json
```

#### 2.4.2.2 body

```
```

### 2.4.3 response

```
{
  "code": 200,
  "msg": "success",
  "data": { 
    "list": [ 
      {
        "id": 1,
        "address": "0x0000000000000000000000000000000000000000",
        "name: "0xaddress",
        "headImageUrl": "https://image.com/headImageUrl",
        "backgroundUrl": "https://image.com/backgroundUrl",
        "createTime": "2022-06-21 05:16:27",
        "tags": [
          {
            "name": "Gold Seller",
            "iconUrl: "https://image.com/iconUrl",
            "createTime": "2022-09-26 15:56:11"
          },
          {
            "name": "Insight Man",
            "iconUrl: "https://image.com/iconUrl",
            "createTime": "2022-09-21 05:16:27"
          }
        ],
        "followingTime": "2022-08-21 15:16:27",
        "following": 10,
        "follower": 3
      },
      {
        "id": 2,
        "address": "0x0000000000000000000000000000000000000001",
        "name: "0xaddress2",
        "headImageUrl": "https://image.com/headImageUrl2",
        "backgroundUrl": "https://image.com/backgroundUrl2",
        "createTime": "2022-07-01 05:16:27",
        "tags": [
          {
            "name": "Gold Seller",
            "iconUrl: "https://image.com/iconUrl",
            "createTime": "2022-09-26 15:56:11"
          }
        ],
        "followingTime": "2022-07-21 15:16:27",
        "following": 10,
        "follower": 3
      }
    ],
    "total": 1,
    "page": 0,
    "pageSize": 10
  }
}
```

## <a id="2-5">2.5 GetUserFollower</a>

### 2.5.1 URL

```
GET /api/v1/user/follower?page=1&pageSize=100&address=0x96216849c49358B10257cb55b28eA603c874b05E
```

### 2.5.2 Request

#### 2.5.2.1 header

```
Content-Type: application/json
```

#### 2.5.2.2 body

```
```

### 2.5.3 response

```
{
  "code": 200,
  "msg": "success",
  "data": {
    "list": [ 
      {
        "id": 1,
        "address": "0x0000000000000000000000000000000000000000",
        "name: "0xaddress",
        "headImageUrl": "https://image.com/headImageUrl",
        "backgroundUrl": "https://image.com/backgroundUrl",
        "createTime": "2022-06-21 05:16:27",
        "tags": [
          {
            "name": "Gold Seller",
            "iconUrl: "https://image.com/iconUrl",
            "createTime": "2022-09-26 15:56:11"
          },
          {
            "name": "Insight Man",
            "iconUrl: "https://image.com/iconUrl",
            "createTime": "2022-09-21 05:16:27"
          }
        ],
        "followerTime": "2022-08-21 15:16:27",
        "following": 10,
        "follower": 3
      },
      {
        "id": 2,
        "address": "0x0000000000000000000000000000000000000001",
        "name: "0xaddress2",
        "headImageUrl": "https://image.com/headImageUrl2",
        "backgroundUrl": "https://image.com/backgroundUrl2",
        "createTime": "2022-07-01 05:16:27",
        "tags": [
          {
            "name": "Gold Seller",
            "iconUrl: "https://image.com/iconUrl",
            "createTime": "2022-09-26 15:56:11"
          }
        ],
        "followerTime": "2022-07-21 15:16:27",
        "following": 10,
        "follower": 3
      }
    ],
    "total": 1,
    "page": 0,
    "pageSize": 10
  }
}
```

## <a id="2-6">2.6 FollowOrUnFollow</a>

### 2.6.1 URL

```
POST /api/v1/user/follow
```

### 2.6.2 Request

#### 2.6.2.1 header

```
Content-Type: application/json
Authorization: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZGRyZXNzIjoiMHg1MjcyNzhBNzUwQTEzZEQ0MTU4QkNCMzFjNWZhODIzYjgxRjYwNERmIiwibmFtZSI6bnVsbCwiaWF0IjoxNjY0MTgzMjU1LCJleHAiOjE2NjQyNjk2NTUsImlzcyI6Ikxvb2tzIFJhcmUifQ.Azw362qxOZwW3HMkWHpEKvwrtuc7EF-Fmm4NIalUksE"
```

#### 2.6.2.2 body

```
{
  "followUser": "0x0000000000000000000000000000000000000001",
}
```

### 2.6.3 response

```
{
  "code": 200,
  "msg": "success",
  "data": "follow/unfollow"
}
```

## <a id="2-7">2.7 GetUserActivity</a>

### 2.7.1 URL

```
POST /api/v1/user/activity?page=1&pageSize=100&relocationAddress=0x43e4f9853e4c4e4cc6d606cfc9cec5a707b1f801

page: [1,~)
pageSize: [1-100]
relocationAddress: user address
```

### 2.7.2 Request

#### 2.7.2.1 header

```
Content-Type: application/json
Authorization: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZGRyZXNzIjoiMHg1MjcyNzhBNzUwQTEzZEQ0MTU4QkNCMzFjNWZhODIzYjgxRjYwNERmIiwibmFtZSI6bnVsbCwiaWF0IjoxNjY0MTgzMjU1LCJleHAiOjE2NjQyNjk2NTUsImlzcyI6Ikxvb2tzIFJhcmUifQ.Azw362qxOZwW3HMkWHpEKvwrtuc7EF-Fmm4NIalUksE"
```

#### 2.7.2.2 body

```

```

### 2.7.3 response

```
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": 1588374438620012544,
                "from": "0x0000000000000000000000000000000000000000",
                "to": "0x43e4f9853e4c4e4cc6d606cfc9cec5a707b1f801",
                "type": "1",
                "address": "0x16c8a1419d60ea926ee1911cfc29a09128e85839",
                "tokenId": "4",
                "price": "",
                "relocationAddress": "0x43e4f9853e4c4e4cc6d606cfc9cec5a707b1f801",
                "time": "2022-11-04T03:35:51Z",
                "chainId": 1,
                "quantity": "",
                "trxHash": "0x71192d5f45cb1b6606e2a45a2d08c981c6584ecfb86c972de56b5ea7b06cfce0",
                "orderHash": ""
            }
        ],
        "total": 1,
        "page": 1,
        "pageSize": 100
    },
    "msg": "success"
}

type: 0.Transfer 1.Mint 2.List 3.Offer 4.Bnpl 5.Cancel 6.Fufill 7.Repay 8.Broken
```

## <a id="2-8">2.8 FavoriteOrUnFavorite</a>

### 2.8.1 URL

```
POST /api/v1/user/favorite
```

### 2.8.2 Request

#### 2.8.2.1 header

```
Content-Type: application/json
Authorization: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZGRyZXNzIjoiMHg1MjcyNzhBNzUwQTEzZEQ0MTU4QkNCMzFjNWZhODIzYjgxRjYwNERmIiwibmFtZSI6bnVsbCwiaWF0IjoxNjY0MTgzMjU1LCJleHAiOjE2NjQyNjk2NTUsImlzcyI6Ikxvb2tzIFJhcmUifQ.Azw362qxOZwW3HMkWHpEKvwrtuc7EF-Fmm4NIalUksE"
```

#### 2.8.2.2 body

```
{
    "contractAddress": "0x8853b05833029e3cf8d3cbb592f9784fa43d2a79",
    "tokenId": "15"
}
```

### 2.8.3 response

```
{
    "code": 200,
    "data": "favorite/unfavorite",
    "msg": "success"
}
```

## <a id="2-9">2.9 GetCollect</a>

### 2.9.1 URL

```
GET /api/v1/user/collect

page: [1,~)
pageSize: [1-100]
keyword: at least 3 charactor
cursor: use the endCursor from the last result set
contractAddress: contract address, filter the same collection
sort: 0.price low to high 1.price high to low 2.recently listed 3.common to rarest 4.rarest to common
status: array, optional value: Buy Now、Has Offers
minPrice: min price
maxPrice: max price
traits: map[string]string
```

### 2.9.2 Request

#### 2.9.2.1 header

```
Content-Type: application/json
Authorization: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZGRyZXNzIjoiMHg1MjcyNzhBNzUwQTEzZEQ0MTU4QkNCMzFjNWZhODIzYjgxRjYwNERmIiwibmFtZSI6bnVsbCwiaWF0IjoxNjY0MTgzMjU1LCJleHAiOjE2NjQyNjk2NTUsImlzcyI6Ikxvb2tzIFJhcmUifQ.Azw362qxOZwW3HMkWHpEKvwrtuc7EF-Fmm4NIalUksE"
```

#### 2.9.2.2 body

```
```

### 2.9.3 response

```
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": "0x5ee38f7ed251fb362ce7130a63a529b533139776-1339",
                "name": "Beast #1339",
                "chain": 1,
                "contractAddress": "0x5ee38f7ed251fb362ce7130a63a529b533139776",
                "tokenId": "1339",
                "description": "",
                "createTime": 0,
                "endTime": 0,
                "lastTransferTime": 1628653110,
                "lastListingTime": 0,
                "price": 0,
                "maxOfferPrice": 0,
                "mintTime": 1628653110,
                "category": 0,
                "currency": "",
                "owner": "0x96216849c49358B10257cb55b28eA603c874b05E",
                "amount": "1",
                "rarity": "",
                "volume": 0,
                "image": "https://gateway.pinata.cloud/ipfs/QmcimtwbWGKXLJ3pTMRu2ncEeeuK9DUwYye6uhJhZC9C6A/beast1339.png",
                "gateway": "https://res.cloudinary.com/alchemyapi/image/upload/mainnet/90defc98ffb6f79d7c000f500ff4ea31.png",
                "thumbnail": "https://res.cloudinary.com/alchemyapi/image/upload/w_256,h_256/mainnet/90defc98ffb6f79d7c000f500ff4ea31.png",
                "tokenUri": "https://alchemy.mypinata.cloud/ipfs/QmY3Lz7DfQPtPkK4n5StZcqc2zA6cmJC7wcAgzYXvGQLGm/1339",
                "attributes": [
                    {
                        "value": "Brown",
                        "trait_type": "Background",
                        "display_type": "",
                        "rarity": ""
                    },
                    {
                        "value": "Red",
                        "trait_type": "Fur",
                        "display_type": "",
                        "rarity": ""
                    },
                    {
                        "value": "Blue Cleats",
                        "trait_type": "Shoes",
                        "display_type": "",
                        "rarity": ""
                    },
                    {
                        "value": "Red Hawaiian Shirt",
                        "trait_type": "Shirt",
                        "display_type": "",
                        "rarity": ""
                    },
                    {
                        "value": "Purple",
                        "trait_type": "Eyes",
                        "display_type": "",
                        "rarity": ""
                    },
                    {
                        "value": "Eyepatch",
                        "trait_type": "Hat",
                        "display_type": "",
                        "rarity": ""
                    },
                    {
                        "value": "Unit I",
                        "trait_type": "Unit",
                        "display_type": "",
                        "rarity": ""
                    }
                ],
                "bgColor": ""
            }
        ],
        "total": 4,
        "page": 1,
        "pageSize": 10,
        "endCursor": [
            "Infinity",
            "0x5ee38f7ed251fb362ce7130a63a529b533139776",
            "1339"
        ],
        "hasNextPage": true
    },
    "msg": "success"
}
```

## <a id="2-10">2.10 GetFavorite</a>

### 2.10.1 URL

```
GET /api/v1/user/favorite

page: [1,~)
pageSize: [1-100]
keyword: at least 3 charactor
cursor: use the endCursor from the last result set
contractAddress: contract address, filter the same collection
sort: 0.price low to high 1.price high to low 2.recently listed 3.common to rarest 4.rarest to common
status: array, optional value: Buy Now、Has Offers
minPrice: min price
maxPrice: max price
traits: map[string]string
```

### 2.10.2 Request

#### 2.10.2.1 header

```
Content-Type: application/json
Authorization: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZGRyZXNzIjoiMHg1MjcyNzhBNzUwQTEzZEQ0MTU4QkNCMzFjNWZhODIzYjgxRjYwNERmIiwibmFtZSI6bnVsbCwiaWF0IjoxNjY0MTgzMjU1LCJleHAiOjE2NjQyNjk2NTUsImlzcyI6Ikxvb2tzIFJhcmUifQ.Azw362qxOZwW3HMkWHpEKvwrtuc7EF-Fmm4NIalUksE"
```

#### 2.10.2.2 body

```
```

### 2.10.3 response

```
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": "0x25baabaf41ce56565f448c6f6e16d44399812cad-1330",
                "name": "Stray Cat #1330",
                "chain": 1,
                "contractAddress": "0x25baabaf41ce56565f448c6f6e16d44399812cad",
                "tokenId": "1330",
                "description": "Stray Cats are a series of 3.000 fearsome hyped beasts amazingly dressed and designed to those who want to look good, invest in NFTs while literally saving animal life.",
                "createTime": 0,
                "endTime": 0,
                "lastTransferTime": 1628644876,
                "lastListingTime": 0,
                "price": 0,
                "maxOfferPrice": 0,
                "mintTime": 1628644876,
                "category": 0,
                "currency": "",
                "owner": "0xfd72ab50c5e80a07a19ae8cfd6b23c4116fecf62",
                "amount": "1",
                "rarity": "",
                "volume": 0,
                "image": "https://straycats.nyc3.digitaloceanspaces.com/images/1330.png",
                "gateway": "https://res.cloudinary.com/alchemyapi/image/upload/mainnet/a9e6515a2b69de4b4527ec7dc99e6483.png",
                "thumbnail": "https://res.cloudinary.com/alchemyapi/image/upload/w_256,h_256/mainnet/a9e6515a2b69de4b4527ec7dc99e6483.png",
                "tokenUri": "https://straycats.nyc3.digitaloceanspaces.com/metadata/1330",
                "attributes": [
                    {
                        "value": "Cloud",
                        "trait_type": "background",
                        "display_type": "",
                        "rarity": ""
                    },
                    {
                        "value": "Orange Stripes",
                        "trait_type": "body",
                        "display_type": "",
                        "rarity": ""
                    },
                    {
                        "value": "Never Tired Tattoo",
                        "trait_type": "skin",
                        "display_type": "",
                        "rarity": ""
                    },
                    {
                        "value": "White Striped Hoodie",
                        "trait_type": "clothes",
                        "display_type": "",
                        "rarity": ""
                    },
                    {
                        "value": "Confused",
                        "trait_type": "face",
                        "display_type": "",
                        "rarity": ""
                    },
                    {
                        "value": "Short Dread",
                        "trait_type": "top",
                        "display_type": "",
                        "rarity": ""
                    },
                    {
                        "value": "Ski Glasses",
                        "trait_type": "accessory",
                        "display_type": "",
                        "rarity": ""
                    }
                ],
                "bgColor": ""
            }
        ],
        "total": 124,
        "page": 1,
        "pageSize": 1,
        "endCursor": [
            "Infinity",
            "0x25baabaf41ce56565f448c6f6e16d44399812cad",
            "1330"
        ],
        "hasNextPage": true
    },
    "msg": "success"
}
```

## <a id="2-11">2.11 UploadPreSignUrl</a>

### 2.11.1 URL

```
GET /api/v1/user/uploadPreSignUrl?type=0&fileExt=png

type: 0.avatar 1.background, default 0
fileExt: the extension of the file to upload
```

### 2.11.2 Request

#### 2.11.2.1 header

```
Content-Type: application/json
Authorization: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZGRyZXNzIjoiMHg1MjcyNzhBNzUwQTEzZEQ0MTU4QkNCMzFjNWZhODIzYjgxRjYwNERmIiwibmFtZSI6bnVsbCwiaWF0IjoxNjY0MTgzMjU1LCJleHAiOjE2NjQyNjk2NTUsImlzcyI6Ikxvb2tzIFJhcmUifQ.Azw362qxOZwW3HMkWHpEKvwrtuc7EF-Fmm4NIalUksE"
```

#### 2.11.2.2 body

```
```

### 2.11.3 response

```
{
    "code": 200,
    "data": {
        "url": "https://apollo-1254079743.cos.ap-hongkong.myqcloud.com/profile/0x96216849c49358B10257cb55b28eA603c874b05E/avatar.png?KeyEndTime=2022-12-08T16%3A21%3A57%2B08%3A00&KeyStartTime=2022-12-08T15%3A16%3A57%2B08%3A00&SignEndTime=2022-12-08T16%3A21%3A57%2B08%3A00&SignStartTime=2022-12-08T15%3A16%3A57%2B08%3A00&q-sign-algorithm=sha1&q-ak=AKIDZzEH7j6f2B5lDTVIrFPKGyShiW5QWO2R&q-sign-time=1670484117%3B1670487717&q-key-time=1670484117%3B1670487717&q-header-list=host&q-url-param-list=keyendtime%3Bkeystarttime%3Bsignendtime%3Bsignstarttime&q-signature=d04eb250c369298694bfa369032cc47466d8651f",
        "expired": 1670487717
    },
    "msg": "success"
}
```

### 2.11.4 Remark

Front-end usage

```
PUT request, use the returned url as the request address, and use binary to upload the file

axios example：
var file = document.getElementById('imageFile').files[0]
var header = {'contentType': file.type}
axios.put(url, file, header)

PS: The image access address is the content before the question mark in the string.
```

## <a id="2-12">2.12 UploadCredential</a>

### 2.12.1 URL

```
GET /api/v1/user/uploadCredential
```

### 2.12.2 Request

#### 2.12.2.1 header

```
Content-Type: application/json
Authorization: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZGRyZXNzIjoiMHg1MjcyNzhBNzUwQTEzZEQ0MTU4QkNCMzFjNWZhODIzYjgxRjYwNERmIiwibmFtZSI6bnVsbCwiaWF0IjoxNjY0MTgzMjU1LCJleHAiOjE2NjQyNjk2NTUsImlzcyI6Ikxvb2tzIFJhcmUifQ.Azw362qxOZwW3HMkWHpEKvwrtuc7EF-Fmm4NIalUksE"
```

#### 2.12.2.2 body

```
```

### 2.12.3 response

```
{
    "code": 200,
    "data": {
        "url": "https://apollo-1254079743.cos.ap-hongkong.myqcloud.com",
        "tmpSecretId": "AKID3zBPRsPDSVnEEw3lRiDeqpMI0ULnVuOKCewC3gEgIvmpnSu9pTsHlwwrGYeXMw9h",
        "tmpSecretKey": "Kmd7CJbTjrI+S5XhVgSBNqJsUOLXVTwH9UI2zn51PjU=",
        "sessionToken": "61dp6l9ewX44BUxKmrbduPzRXnwip4ea4fec14a2e358074cdd7e02a3d9deec92xC2Q5o_HPJs5UXKE3L1hoiC-OW4XEWhob9MdrQD3bmML-DydUBmAGCX0mQBahsAPfQQq-wxKTYnjsucunrCt3ZJvQscyCLdSKFkjKvDtgH2Aeq8xbOdNBUP53hteBSJAtYRfkyvQsGY3peJqrzUimUbPV_oXP20O6ZEUhLSo_NALN1zfmAxQA8Yo-T4dNn1l6yF3XeTCwGTjY0G87ubQsm2GKubzQBA1SaqvSG-WbbqYv1yGaebDy8qySXW6A2gKT1OwqLNH06Llok_bhhyQ-RzpRloR0-UUPPNl6_AtnjCjYFPXLUFeOFG37q-PQJ287rn3SQ38HlDzT9H0AB6VFiT66yyjWrbcmLRo1ksuOv_Jcr4CXAZ8yHFjgt7Ka8t80ZKsakjxryZL8yANSIjT5L7ew9sxkaor4XrT_cmfL3OSaPr77AWVw917vosJ_4wc",
        "expired": 1670488627,
        "avatarPrefix": "profile/0x96216849c49358B10257cb55b28eA603c874b05E/avatar.",
        "backgroundPrefix": "profile/0x96216849c49358B10257cb55b28eA603c874b05E/background."
    },
    "msg": "success"
}
```

### 2.12.4 Remark

Front-end usage

```
tencentcloud docs: https://www.tencentcloud.com/zh/document/product/436/45242#.E4.BD.BF.E7.94.A8.E4.B8.B4.E6.97.B6.E5.AF.86.E9.92.A5.E8.AE.BF.E9.97.AE-cos
sdk: https://github.com/tencentyun/cos-js-sdk-v5
```


# 3. Ranking APIs

## <a id="3-1">3.1 GetCollectionRanking</a>

### 3.1.1 URL

```
GET /api/v1/ranking/collection?page=1&pageSize=1&type=0&sort=0

type: 0.volume_1d 1.volume_7d 2.volume_30d 3.volume_total, default 0
sort: 0.volume 1.collection 2.floorPrice 3.change 4.listings 5.items, default 0
direction: 0.desc 1.asc, default 0
```

### 3.1.2 Request

#### 3.1.2.1 header

```
Content-Type: application/json
```

#### 3.1.2.2 body

```
```

### 3.1.3 response

```
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": 61201,
                "createBy": "",
                "updateBy": "",
                "createTime": "2022-12-02T00:48:15Z",
                "updateTime": "2022-12-02T13:03:28Z",
                "type": 0,
                "contractAddress": "",
                "contractName": "RTFKT Animus Egg 🥚",
                "slug": "rtfkt-animus-egg",
                "logoUrl": "https://i.seadn.io/gcs/files/44e8866f6b904542b7bb59dc12af64f2.gif?w=500&auto=format",
                "bannerUrl": "",
                "itemsTotal": 6878,
                "ownersTotal": 3530,
                "salesTotal": 211,
                "sales": 726,
                "volume": 814.0665,
                "volume1d": 814.066498,
                "volume7d": 814.066498,
                "volume30d": 814.066498,
                "volumeTotal": 814.066498,
                "floorPrice": 1.128,
                "averagePrice1d": 0,
                "averagePrice7d": 0,
                "averagePrice30d": 0,
                "averagePriceTotal": 0,
                "volumeChange": 0,
                "volumeChange1d": 0,
                "volumeChange7d": 0,
                "hidden": false
            }
        ],
        "total": 127,
        "page": 1,
        "pageSize": 1
    },
    "msg": "success"
}
```

## <a id="3-2">3.2 GetCollectionTrending</a>

### 3.2.1 URL

```
GET /api/v1/trending/collection

type: 0.15m 1.30m 2.1h 3.6h 4.12h 5.1d 6.7d 7.30d
```

### 3.2.2 Request

#### 3.2.2.1 header

```
Content-Type: application/json
```

#### 3.2.2.2 body

```
```

### 3.2.3 response

```
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": 62,
                "createBy": "",
                "updateBy": "",
                "createTime": "2022-11-25T18:05:08Z",
                "updateTime": "2022-11-25T18:05:08Z",
                "type": 1,
                "range_type": 5,
                "average_price": 0.0135,
                "average_price_change": "1.35%",
                "contract_address": "0x73350fdf1bfd08555d6fe440d3ffa87104d1da19",
                "contract_name": "Colizeum ELITE",
                "exchange_volume_change_24h": "100.0000%",
                "exchange_volume_change_7d": "100.0000%",
                "floor_price": 0.0239,
                "highest_price": 0.195,
                "items_total": 5000,
                "logo_url": "https://logo.nftscan.com/logo/0x73350fdf1bfd08555d6fe440d3ffa87104d1da19.png",
                "lowest_price": 0.0021,
                "market_cap": 66.5,
                "market_trend": "6750.00%",
                "mint_average_price": 0,
                "mint_gas_fee": 21.7035,
                "mint_price_total": 0,
                "owners_total": 2298,
                "price_7d": [
                    {
                        "average_Price": 0,
                        "begin_Timestamp": 1668787200000,
                        "end_Timestamp": 1668873600000
                    },
                    {
                        "average_Price": 0,
                        "begin_Timestamp": 1668873600000,
                        "end_Timestamp": 1668960000000
                    },
                    {
                        "average_Price": 0,
                        "begin_Timestamp": 1668960000000,
                        "end_Timestamp": 1669046400000
                    },
                    {
                        "average_Price": 0,
                        "begin_Timestamp": 1669046400000,
                        "end_Timestamp": 1669132800000
                    },
                    {
                        "average_Price": 0,
                        "begin_Timestamp": 1669132800000,
                        "end_Timestamp": 1669219200000
                    },
                    {
                        "average_Price": 0,
                        "begin_Timestamp": 1669219200000,
                        "end_Timestamp": 1669305600000
                    },
                    {
                        "average_Price": 0.0149,
                        "begin_Timestamp": 1669305600000,
                        "end_Timestamp": 1669392000000
                    }
                ],
                "sales": 3599,
                "volume": 48.5181,
                "volume_7d": [
                    {
                        "volume": 0,
                        "begin_Timestamp": 1668787200000,
                        "end_Timestamp": 1668873600000
                    },
                    {
                        "volume": 0,
                        "begin_Timestamp": 1668873600000,
                        "end_Timestamp": 1668960000000
                    },
                    {
                        "volume": 0,
                        "begin_Timestamp": 1668960000000,
                        "end_Timestamp": 1669046400000
                    },
                    {
                        "volume": 0,
                        "begin_Timestamp": 1669046400000,
                        "end_Timestamp": 1669132800000
                    },
                    {
                        "volume": 0,
                        "begin_Timestamp": 1669132800000,
                        "end_Timestamp": 1669219200000
                    },
                    {
                        "volume": 0,
                        "begin_Timestamp": 1669219200000,
                        "end_Timestamp": 1669305600000
                    },
                    {
                        "volume": 41.25544800792525,
                        "begin_Timestamp": 1669305600000,
                        "end_Timestamp": 1669392000000
                    }
                ],
                "volume_change": "4851.81%"
            }
        ],
        "total": 321,
        "page": 1,
        "pageSize": 100
    },
    "msg": "success"
}
```

# 4. NFT APIs

## <a id="4-1">4.1 Search</a>

### 4.1.1 URL

```
GET /api/v1/search

isSummary: true - search top 5 collection、nft、user; false - search collection/nft/user
page: [1,~)
pageSize: [1-100]
type: 0.collection 1.nft 2.user
keyword: at least 3 charactor
cursor: use the endCursor from the last result set
```

### 4.1.2 Request

#### 4.1.2.1 header

```
Content-Type: application/json
```

#### 4.1.2.2 body

```
```

### 4.1.3 response

isSummary: true
```
{
    "code": 200,
    "data": {
        "collections": [
            {
                "id": "0x15820072729d045ec5232ba3bd060ec5df38e09a",
                "name": "Tavern NFT",
                "contractAddress": "0x15820072729d045ec5232ba3bd060ec5df38e09a",
                "symbol": "Tavern",
                "chain": 1,
                "tokenType": "ERC721",
                "contractName": "",
                "safelistRequestStatus": "",
                "description": "",
                "floorPrice": 0,
                "image": "",
                "owner": "",
                "twitter": "",
                "discord": "",
                "instagram": "",
                "website": "",
                "totalSupply": "30",
                "tradeTimes": 0,
                "volume": 0
            }
        ],
        "nfts": [
            {
                "id": "0x15820072729d045ec5232ba3bd060ec5df38e09a-0",
                "name": "[SS][Genesis]Oriental Pearl Tower",
                "chain": 1,
                "contractAddress": "0x15820072729d045ec5232ba3bd060ec5df38e09a",
                "tokenId": "0",
                "description": "1 Century Ave, LuJiaZui \n longitude 121.495376 \n latitude 31.241680",
                "createTime": 0,
                "endTime": 0,
                "lastTransferTime": 1536058925,
                "lastListingTime": 0,
                "price": 0,
                "maxOfferPrice": 0,
                "mintTime": 1536054087,
                "category": 0,
                "currency": "",
                "owner": "0x744a31ede5422355d9c2bd8c44c710404336ca84",
                "amount": "1",
                "rarity": "",
                "volume": 0,
                "image": "https://lordless-sh.oss-cn-shanghai.aliyuncs.com/Metadata/Image/0.png",
                "gateway": "https://lordless-sh.oss-cn-shanghai.aliyuncs.com/Metadata/Image/0.png",
                "thumbnail": "",
                "tokenUri": "https://game.lordless.io/api/tavern/status/0",
                "attributes": [
                    {
                        "value": "SS",
                        "trait_type": "popularity"
                    },
                    {
                        "value": "Shanghai",
                        "trait_type": "city"
                    },
                    {
                        "value": "China",
                        "trait_type": "country"
                    },
                    {
                        "value": "1218",
                        "trait_type": "Action point remaining"
                    },
                    {
                        "value": "942",
                        "trait_type": "Bounty Hunters"
                    }
                ]
            }
        ],
        "users": [
            {
                "id": 1,
                "createBy": "",
                "updateBy": "",
                "createTime": "0001-01-01T00:00:00Z",
                "updateTime": "0001-01-01T00:00:00Z",
                "address": "0x96216849c49358B10257cb55b28eA603c874b05E",
                "name": "0x96216849c49358B10257cb55b28eA603c874b05E",
                "headImageUrl": "",
                "backgroundUrl": "",
                "following": 0,
                "follower": 0
            }
        ]
    },
    "msg": "success"
}
```

isSummary: false, type: 0
```
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": "0x15820072729d045ec5232ba3bd060ec5df38e09a",
                "name": "Tavern NFT",
                "contractAddress": "0x15820072729d045ec5232ba3bd060ec5df38e09a",
                "symbol": "Tavern",
                "chain": 1,
                "tokenType": "ERC721",
                "contractName": "",
                "safelistRequestStatus": "",
                "description": "",
                "floorPrice": 0,
                "image": "",
                "owner": "",
                "twitter": "",
                "discord": "",
                "instagram": "",
                "website": "",
                "totalSupply": "30",
                "tradeTimes": 0,
                "volume": 0
            }
        ],
        "total": 30,
        "page": 1,
        "pageSize": 10,
        "endCursor": [
            "-Infinity",
            "0x5caebd3b32e210e85ce3e9d51638b9c445481567"
        ],
        "hasNextPage": true
    },
    "msg": "success"
}
```

isSummary: false, type: 1
```
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": "0x15820072729d045ec5232ba3bd060ec5df38e09a-0",
                "name": "[SS][Genesis]Oriental Pearl Tower",
                "chain": 1,
                "contractAddress": "0x15820072729d045ec5232ba3bd060ec5df38e09a",
                "tokenId": "0",
                "description": "1 Century Ave, LuJiaZui \n longitude 121.495376 \n latitude 31.241680",
                "createTime": 0,
                "endTime": 0,
                "lastTransferTime": 1536058925,
                "lastListingTime": 0,
                "price": 0,
                "maxOfferPrice": 0,
                "mintTime": 1536054087,
                "category": 0,
                "currency": "",
                "owner": "0x744a31ede5422355d9c2bd8c44c710404336ca84",
                "amount": "1",
                "rarity": "",
                "volume": 0,
                "image": "https://lordless-sh.oss-cn-shanghai.aliyuncs.com/Metadata/Image/0.png",
                "gateway": "https://lordless-sh.oss-cn-shanghai.aliyuncs.com/Metadata/Image/0.png",
                "thumbnail": "",
                "tokenUri": "https://game.lordless.io/api/tavern/status/0",
                "attributes": [
                    {
                        "value": "SS",
                        "trait_type": "popularity"
                    },
                    {
                        "value": "Shanghai",
                        "trait_type": "city"
                    },
                    {
                        "value": "China",
                        "trait_type": "country"
                    },
                    {
                        "value": "1218",
                        "trait_type": "Action point remaining"
                    },
                    {
                        "value": "942",
                        "trait_type": "Bounty Hunters"
                    }
                ]
            }
        ],
        "total": 7689,
        "page": 1,
        "pageSize": 10,
        "endCursor": [
            "-Infinity",
            "0x15820072729d045ec5232ba3bd060ec5df38e09a",
            "1805"
        ],
        "hasNextPage": true
    },
    "msg": "success"
}
```

isSummary: false, type: 2
```
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": 1,
                "createBy": "",
                "updateBy": "",
                "createTime": "0001-01-01T00:00:00Z",
                "updateTime": "0001-01-01T00:00:00Z",
                "address": "0x96216849c49358B10257cb55b28eA603c874b05E",
                "name": "0x96216849c49358B10257cb55b28eA603c874b05E",
                "headImageUrl": "",
                "backgroundUrl": "",
                "following": 0,
                "follower": 0
            }
        ],
        "total": 1,
        "page": 1,
        "pageSize": 10,
        "endCursor": null,
        "hasNextPage": false
    },
    "msg": "success"
}
```

## <a id="4-2">4.2 GetCollectionByAddress</a>

### 4.2.1 URL

```
GET /api/v1/collection/0x8853b05833029e3cf8d3cbb592f9784fa43d2a79
```

### 4.2.2 Request

#### 4.2.2.1 header

```
Content-Type: application/json
```

#### 4.2.2.2 body

```
```

### 4.2.3 response

```
{
    "code": 200,
    "data": {
        "id": "0x8853b05833029e3cf8d3cbb592f9784fa43d2a79",
        "name": "Codex Record",
        "contractAddress": "0x8853b05833029e3cf8d3cbb592f9784fa43d2a79",
        "symbol": "CR",
        "chain": 1,
        "tokenType": "ERC721",
        "contractName": "",
        "safelistRequestStatus": "",
        "description": "",
        "floorPrice": 0,
        "image": "",
        "owner": "",
        "twitter": "",
        "discord": "",
        "instagram": "",
        "website": "",
        "totalSupply": "493000",
        "tradeTimes": 0,
        "volume": 0
    },
    "msg": "success"
}
```

## <a id="4-3">4.3 GetCollectionActivity</a>

### 4.3.1 URL

```
POST /api/v1/collection/activity?page=1&pageSize=100&relocationAddress=0x16c8a1419d60ea926ee1911cfc29a09128e85839

page: [1,~)
pageSize: [1-100]
relocationAddress: use "collection contract address" to get collection activity; use "collection contract address + nft id" to get nft activity
```

### 4.3.2 Request

#### 4.3.2.1 header

```
Content-Type: application/json
```

#### 4.3.2.2 body

```

```

### 4.3.3 response

```
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": 1588374438638170112,
                "from": "0x0000000000000000000000000000000000000000",
                "to": "0x43e4f9853e4c4e4cc6d606cfc9cec5a707b1f801",
                "type": "1",
                "address": "0x16c8a1419d60ea926ee1911cfc29a09128e85839",
                "tokenId": "4",
                "price": "",
                "relocationAddress": "0x16c8a1419d60ea926ee1911cfc29a09128e85839",
                "time": "2022-11-04T03:35:51Z",
                "chainId": 1,
                "quantity": "",
                "trxHash": "0x71192d5f45cb1b6606e2a45a2d08c981c6584ecfb86c972de56b5ea7b06cfce0",
                "orderHash": ""
            }
        ],
        "total": 1,
        "page": 1,
        "pageSize": 100
    },
    "msg": "success"
}

type: 0.Transfer 1.Mint 2.List 3.Offer 4.Bnpl 5.Cancel 6.Fufill 7.Repay 8.Broken
```

## <a id="4-4">4.4 SearchNft</a>

### 4.4.1 URL

```
GET /api/v1/nfts

page: [1,~)
pageSize: [1-100]
keyword: at least 3 charactor
cursor: use the endCursor from the last result set
contractAddress: contract address, filter the same collection
sort: 0.price low to high 1.price high to low 2.recently listed 3.common to rarest 4.rarest to common
status: array, optional value: Buy Now、Has Offers
minPrice: min price
maxPrice: max price
traits: map[string]string
```

### 4.4.2 Request

#### 4.4.2.1 header

```
Content-Type: application/json
```

#### 4.4.2.2 body

```
```

### 4.4.3 response

```
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": "0x8853b05833029e3cf8d3cbb592f9784fa43d2a79-100",
                "name": "Codex Record #100",
                "chain": 1,
                "contractAddress": "0x8853b05833029e3cf8d3cbb592f9784fa43d2a79",
                "tokenId": "100",
                "description": "A Private Record in the Codex Registry",
                "createTime": 0,
                "endTime": 0,
                "lastTransferTime": 1532759478,
                "lastListingTime": 0,
                "price": 0,
                "maxOfferPrice": 0,
                "mintTime": 1532759478,
                "category": 0,
                "currency": "",
                "owner": "0xf7b10d603907658f690da534e9b7dbc4dab3e2d6",
                "amount": "1",
                "rarity": "",
                "volume": 0,
                "image": "https://s3-us-west-2.amazonaws.com/codex.registry-production/assets/generic-record-image.png",
                "gateway": "https://s3-us-west-2.amazonaws.com/codex.registry-production/assets/generic-record-image.png",
                "thumbnail": "",
                "tokenUri": "https://api.codexprotocol.com/token-metadata/100",
                "attributes": []
            }
        ],
        "total": 513,
        "page": 1,
        "pageSize": 10,
        "endCursor": [
            "Infinity",
            "0x8853b05833029e3cf8d3cbb592f9784fa43d2a79",
            "109"
        ],
        "hasNextPage": true
    },
    "msg": "success"
}
```

## <a id="4-5">4.5 GetNftByTokenId</a>

### 4.5.1 URL

```
GET /api/v1/nft?contractAddress=0x8853b05833029e3cf8d3cbb592f9784fa43d2a79&tokenId=15

contractAddress: contract address
tokenId: token ID
```

### 4.5.2 Request

#### 4.5.2.1 header

```
Content-Type: application/json
```

#### 4.5.2.2 body

```
```

### 4.5.3 response

```
{
    "code": 200,
    "data": {
        "id": "0x6050cc330bf64f090ebea02411ccf6a850cb9273-5146",
        "name": "Starborn #5144",
        "chain": 1,
        "contractAddress": "0x6050cc330bf64f090ebea02411ccf6a850cb9273",
        "tokenId": "5146",
        "description": "Starborn #5144",
        "createTime": 0,
        "endTime": 0,
        "lastTransferTime": 1628644538,
        "lastListingTime": 0,
        "price": 0,
        "maxOfferPrice": 0,
        "mintTime": 1628644538,
        "category": 0,
        "currency": "",
        "owner": "0xeb602be2f3a58be84a77ac01ab6ab0ce0795e238",
        "amount": "1",
        "rarity": "",
        "volume": 0,
        "image": "ipfs://QmTEgYuad4ubvhMG6REx9gmCHRxKirzSQdB9hGhctJvmi6/5144.png",
        "gateway": "ipfs://QmTEgYuad4ubvhMG6REx9gmCHRxKirzSQdB9hGhctJvmi6/5144.png",
        "thumbnail": "",
        "tokenUri": "https://alchemy.mypinata.cloud/ipfs/QmNZipSHhMXWx7h7mc3xT7aWkGkwLVgyRdeUePi7nJqo5S/5144",
        "attributes": [
            {
                "value": "Scientist",
                "trait_type": "Class",
                "display_type": "",
                "rarity": "19.77%"
            },
            {
                "value": "Streamlined",
                "trait_type": "Class Variant",
                "display_type": "",
                "rarity": "50.26%"
            }
        ],
        "bgColor": "",
        "chainName": "Ethereum Mainnet",
        "views": 8,
        "favorites": 0,
        "contractName": "",
        "ownerName": "0xeb602be2f3a58be84a77ac01ab6ab0ce0795e238",
        "salesEnd": "",
        "currentPrice": "",
        "currentPriceUsd": "",
        "safelistRequestStatus": "",
        "serviceFee": 0.025,
        "creatorFee": 0,
        "usdPrice": 1252.01
    },
    "msg": "success"
}
```

## <a id="4-6">4.6 GetNftCondition</a>

### 4.6.1 URL

```
GET /api/v1/nftCondition?contractAddress=0x71772beff1fb348eb7d5f9f1e0b5f11bc49ab5e4&showCollection=true

contractAddress: contract address, filter collection traits
showCollection: true - return collection result set; false - not return collection result set
```

### 4.6.2 Request

#### 4.6.2.1 header

```
Content-Type: application/json
```

#### 4.6.2.2 body

```
```

### 4.6.3 response

```
{
    "code": 200,
    "data": {
        "status": [
            "Buy Now",
            "Has Offers"
        ],
        "collections": [
            {
                "id": "0xaba31c041e916e4141036f080b554d40cdb2bcd0",
                "name": "Chinese Opera Mask Plus",
                "contractAddress": "0xaba31c041e916e4141036f080b554d40cdb2bcd0",
                "chain": 1,
                "contractName": "",
                "safelistRequestStatus": "",
                "totalSupply": "10000",
                "tradeTimes": 0,
                "volume": 2
            }
        ],
        "traits": {
            "Skin Tone": {
                "ORANGE SKIN TONE": 1111,
                "PINK SKIN TONE": 161,
                "TEAL SKIN TONE": 656,
                "WHITE SKIN TONE": 1335,
                "YELLOW SKIN TONE": 2131
            }
        }
    },
    "msg": "success"
}
```

## <a id="4-7">4.7 GetCollectionCondition</a>

### 4.7.1 URL

```
GET /api/v1/collectionCondition?keyword=nft

keyword: search keyword
```

### 4.7.2 Request

#### 4.7.2.1 header

```
Content-Type: application/json
```

#### 4.7.2.2 body

```
```

### 4.7.3 response

```
{
    "code": 200,
    "data": [
        {
            "id": "0xaba31c041e916e4141036f080b554d40cdb2bcd0",
            "name": "Chinese Opera Mask Plus",
            "contractAddress": "0xaba31c041e916e4141036f080b554d40cdb2bcd0",
            "chain": 1,
            "contractName": "",
            "safelistRequestStatus": "",
            "totalSupply": "10000",
            "tradeTimes": 0,
            "volume": 2
        },
        {
            "id": "0xa7aea29c280a75b67b45764cbf84e7eb2a3eeda9",
            "name": "brokenToken 中华人民共和国成立 Mask Plus",
            "contractAddress": "0xa7aea29c280a75b67b45764cbf84e7eb2a3eeda9",
            "chain": 1,
            "contractName": "",
            "safelistRequestStatus": "",
            "totalSupply": "11",
            "tradeTimes": 0,
            "volume": 1
        }
    ],
    "msg": "success"
}
```

## <a id="4-8">4.8 GetMoreNft</a>

### 4.8.1 URL

```
GET /api/v1/moreNft?contractAddress=0xef482ff2f7874bf6cc679a6b49c020441acd5f2c

contractAddress: contract address
```

### 4.8.2 Request

#### 4.8.2.1 header

```
Content-Type: application/json
```

#### 4.8.2.2 body

```
```

### 4.8.3 response

```
{
    "code": 200,
    "data": {
        "collection": {
            "id": "0x7d256d82b32d8003d1ca1a1526ed211e6e0da9e2",
            "name": "Yat NFT",
            "contractAddress": "0x7d256d82b32d8003d1ca1a1526ed211e6e0da9e2",
            "slug": "",
            "symbol": "Yats",
            "chain": 1,
            "tokenType": "ERC721",
            "contractName": "",
            "safelistRequestStatus": "",
            "description": "",
            "floorPrice": 0,
            "image": "",
            "banner": "",
            "owner": "",
            "twitter": "",
            "discord": "",
            "instagram": "",
            "website": "",
            "totalSupply": "12390",
            "tradeTimes": 0,
            "volume": 0,
            "royaltyAddress": "",
            "royaltyFee": "",
            "chainName": "Ethereum Mainnet"
        },
        "nfts": [
            {
                "id": "0x7d256d82b32d8003d1ca1a1526ed211e6e0da9e2-3511",
                "name": "👻💎👑 | Ghostface Diamond King",
                "chain": 1,
                "contractAddress": "0x7d256d82b32d8003d1ca1a1526ed211e6e0da9e2",
                "tokenId": "3511",
                "description": "Yats 🖖 are emoji usernames that become your universal Internet identity 🗿, website URL 💻, payment address 🤑, and more. By owning a Yat – let’s say 👻💎👑 – it’s yours forever. Get inspired and join our amazingly creative Yat Community at Y.at.",
                "createTime": 0,
                "endTime": 0,
                "lastTransferTime": 1628644538,
                "lastListingTime": 0,
                "price": 0,
                "maxOfferPrice": 0,
                "mintTime": 1628644538,
                "category": 0,
                "currency": "",
                "owner": "0xeb602be2f3a58be84a77ac01ab6ab0ce0795e238",
                "amount": "1",
                "rarity": "",
                "volume": 0,
                "image": "https://y.at/viz/ghost.diamond.crown-2d5e58.png",
                "gateway": "https://y.at/viz/ghost.diamond.crown-2d5e58.png",
                "thumbnail": "",
                "tokenUri": "https://a.y.at/nft_transfers/metadata/3511",
                "attributes": [
                    {
                        "value": "Three-Emoji",
                        "trait_type": "Length",
                        "display_type": "",
                        "rarity": ""
                    },
                    {
                        "value": "71-75",
                        "trait_type": "Rhythm Score",
                        "display_type": "",
                        "rarity": ""
                    },
                    {
                        "value": "Gen Zero",
                        "trait_type": "Generation",
                        "display_type": "",
                        "rarity": ""
                    },
                    {
                        "value": "Light Field",
                        "trait_type": "Visualizer Theme",
                        "display_type": "",
                        "rarity": ""
                    }
                ],
                "bgColor": ""
            }
        ]
    },
    "msg": "success"
}
```

# 5. NFT APIs

## <a id="5-1">5.1 GetNFTPopular</a>

### 5.1.1 URL

```
GET /api/v1/nft/popular
```

### 5.1.2 Request

#### 5.1.2.1 header

```
Content-Type: application/json
```

#### 5.1.2.2 body

```
```

### 5.1.3 response

```
{
  "code": 200,
  "msg": "success",
  "data": {
    "list": [
      {
        "name": "Bored Ape Yacht Club",
        "desc": "Bored Ape Yacht Club is an project...",
        "nftNo: "6417",
        "nftImgUrl": "/uploads/file/bored_ape_yacht_club.png",
        "holder": "0x0000000000000000000000000000000000000000",
        "holderName": "Tom",
        "holderOnline": 1, // 0. offline; 1. Online
        "price": "10",
        "unit": "ETH"
      },
      {
        "name": "Bored Ape Club",
        "desc": "Bored Ape Club is an project...",
        "nftNo: "6417",
        "nftImgUrl": "/uploads/file/bored_ape_yacht_club.png",
        "holder": "0x0000000000000000000000000000000000000001",
        "holderName": "Gim",
        "holderOnline": 0, // 0. offline; 1. Online
        "price": "6",
        "unit": "ETH"
      }
    ],
    "total": 1,
    "page": 0,
    "pageSize": 10
  }
}
```

# 6. Order APIs

## <a id="6-1">6.1 GetOrder</a>

### 6.1.1 URL

```
GET /api/v1/order?page=1&pageSize=10&category=1&contractAddress=0x9c7be9db775d3ff1c67787c4eac29cf46f3ffbfa&tokenId=1

category: 0.listing 1.offer 2.bnpl
contractAddress: contract address
tokenId: token id
```

### 6.1.2 Request

#### 6.1.2.1 header

```
Content-Type: application/json
```

#### 6.1.2.2 body

```
{
  "page": 1,
  "pageSize": 10
}
```

### 6.1.3 response

```
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": 3,
                "assetAmount": 1,
                "assetContractAddress": "0x583A9a2fA2dA85bA0c7ee41b14B889fA4D3c3259",
                "assetId": 3,
                "canceled": false,
                "chainId": 97,
                "clientSignature": "0x547109e064ae70f7c5bb1b4b1db9ad3dcb863b60af0e0cf442e3a2ef7e297141766c3a8a1f316e650b62d7dbe5c52a838dd0d3907595511d4b7ef67bacbfe68a1b",
                "closedAt": "1970-01-01T00:00:00Z",
                "counter": 0,
                "currentPrice": "0",
                "expirationTime": "1697784230",
                "finalized": false,
                "listingTime": "1666248230",
                "maker": "",
                "markedInvalid": false,
                "orderHash": "0x038c2219950de8a9076ec352687a9196c998e1710a5b0b035c062a8d93ce519f",
                "orderType": 0,
                "protocolAddress": "0xD507598932C9C75Db8919C65961100c9f7f32873",
                "protocolData": {
                    "Offerer": "0x0000000000000000000000000000000000000000",
                    "Zone": "0x0000000000000000000000000000000000000000",
                    "Offer": null,
                    "Consideration": null,
                    "OrderType": 0,
                    "StartTime": null,
                    "EndTime": null,
                    "ZoneHash": [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
                    "Salt": null,
                    "ConduitKey": [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
                    "TotalOriginalConsiderationItems": null,
                    "Counter": null
                },
                "side": 0,
                "taker": "0x70e6821f674befb152f1b2ad7017ee89eb55e222",
                "transactionHash": "",
                "createdAt": "2022-10-23T02:12:13.153Z",
                "updatedAt": "2022-10-23T02:12:13.153Z"
            }
        ],
        "total": 1,
        "page": 1,
        "pageSize": 10
    },
    "msg": "success"
}
```

## <a id="6-2">6.2 Listing</a>

### 6.2.1 URL

```
POST /api/v1/order/listing
```

### 6.2.2 Request

#### 6.2.2.1 header

```
Content-Type: application/json
Authorization: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZGRyZXNzIjoiMHg1MjcyNzhBNzUwQTEzZEQ0MTU4QkNCMzFjNWZhODIzYjgxRjYwNERmIiwibmFtZSI6bnVsbCwiaWF0IjoxNjY0MTgzMjU1LCJleHAiOjE2NjQyNjk2NTUsImlzcyI6Ikxvb2tzIFJhcmUifQ.Azw362qxOZwW3HMkWHpEKvwrtuc7EF-Fmm4NIalUksE"
```

#### 6.2.2.2 body

```
network: ethereum、chapel、goerli

{
    "network": "chapel",
    "signature": "0x253842900f2f385a8e85f3cab0f355f53298d747477058774c59b0917c5475b10b212c5adfd446e743d00d6dcb12280f8c19faee7db53c9a454a04a517a80818",
    "offerer": "0x43e4F9853e4C4E4Cc6D606cFC9cec5A707B1F801",
    "zone": "0x0000000000000000000000000000000000000000",
    "zoneHash": "0x3000000000000000000000000000000000000000000000000000000000000000",
    "startTime": 1666248230,
    "endTime": 1697784230,
    "orderType": 0,
    "offer": [
        {
            "itemType": 2,
            "token": "0x0dC72d7E50e46c495245EDca3ca4d291b8A91885",
            "identifierOrCriteria": "3",
            "startAmount": "1",
            "endAmount": "1"
        }
    ],
    "consideration": [
        {
            "itemType": 0,
            "token": "0x0000000000000000000000000000000000000000",
            "identifierOrCriteria": "0",
            "startAmount": "10",
            "endAmount": "10",
            "recipient": "0x43e4F9853e4C4E4Cc6D606cFC9cec5A707B1F801"
        }
    ],
    "totalOriginalConsiderationItems": 1,
    "salt": "0x26186debf8e1ce980be0bddd0d7b0b76",
    "conduitKey": "0x1904BFcb93EdC9BF961Eead2e5c0de81dCc1D37D000000000000000000000000",
    "counter": 0
}
```

### 6.2.3 response

```
{
    "code": 200,
    "data": {},
    "msg": "success"
}
```

## <a id="6-3">6.3 Offer</a>

### 6.3.1 URL

```
POST /api/v1/order/offer
```

### 6.3.2 Request

#### 6.3.2.1 header

```
Content-Type: application/json
Authorization: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZGRyZXNzIjoiMHg1MjcyNzhBNzUwQTEzZEQ0MTU4QkNCMzFjNWZhODIzYjgxRjYwNERmIiwibmFtZSI6bnVsbCwiaWF0IjoxNjY0MTgzMjU1LCJleHAiOjE2NjQyNjk2NTUsImlzcyI6Ikxvb2tzIFJhcmUifQ.Azw362qxOZwW3HMkWHpEKvwrtuc7EF-Fmm4NIalUksE"
```

#### 6.3.2.2 body

```
network: ethereum、chapel、goerli

{
    "network": "chapel",
    "signature": "0xbd4671af7d6ef3faead2b224df232920214328654a702454f4bc3aad9affda6021e7f781987b1203b9640aaae2fb3b8d8a8e1faa1d1f281be67bf4d8876cd37b",
    "offerer": "0x43e4F9853e4C4E4Cc6D606cFC9cec5A707B1F801",
    "zone": "0x0000000000000000000000000000000000000000",
    "zoneHash": "0x3000000000000000000000000000000000000000000000000000000000000000",
    "startTime": 1666248230,
    "endTime": 1697784230,
    "orderType": 0,
    "offer": [
        {
            "itemType": 1,
            "token": "0xae13d989dac2f0debff460ac112a837c89baa7cd",
            "identifierOrCriteria": "0",
            "startAmount": "10000",
            "endAmount": "10000"
        }
    ],
    "consideration": [
        {
            "itemType": 2,
            "token": "0x583A9a2fA2dA85bA0c7ee41b14B889fA4D3c3259",
            "identifierOrCriteria": "3",
            "startAmount": "1",
            "endAmount": "1",
            "recipient": "0x43e4F9853e4C4E4Cc6D606cFC9cec5A707B1F801"
        }
    ],
    "totalOriginalConsiderationItems": 1,
    "salt": "123",
    "conduitKey": "0x1904BFcb93EdC9BF961Eead2e5c0de81dCc1D37D000000000000000000000000",
    "counter": 0
}
```

### 6.3.3 response

```
{
    "code": 200,
    "data": {},
    "msg": "success"
}
```

## <a id="6-4">6.4 CreateBnpl</a>

### 6.4.1 URL

```
POST /api/v1/order/bnpl
```

### 6.4.2 Request

#### 6.4.2.1 header

```
Content-Type: application/json
Authorization: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZGRyZXNzIjoiMHg1MjcyNzhBNzUwQTEzZEQ0MTU4QkNCMzFjNWZhODIzYjgxRjYwNERmIiwibmFtZSI6bnVsbCwiaWF0IjoxNjY0MTgzMjU1LCJleHAiOjE2NjQyNjk2NTUsImlzcyI6Ikxvb2tzIFJhcmUifQ.Azw362qxOZwW3HMkWHpEKvwrtuc7EF-Fmm4NIalUksE"
```

#### 6.4.2.2 body

```
network: ethereum、chapel、goerli

{
    "network": "chapel",
    "signature": "0x97a63c92d0f41cbdfb92a33801fc425814f4b57331cf343a0e2e6d05a4d7d21670ba8263c5c846ba95f99793aa6b95c673abeb62a2638b064ece318367d2749e",
    "offerer": "0x70e6821f674BeFB152F1b2ad7017EE89Eb55E222",
    "token": "0x3cbBaB1d1D2f0F2bd9E331f12002D597a1d80f3E",
    "identifier": "1",
    "currency": "0x0000000000000000000000000000000000000000",
    "artist": "0x43e4F9853e4C4E4Cc6D606cFC9cec5A707B1F801",
    "platform": "0x70e6821f674BeFB152F1b2ad7017EE89Eb55E222",
    "startTime": "1666248230",
    "endTime": "1697784230",
    "duration": "2592000",
    "periods": "3",
    "amount": "10000000000000000000",
    "ratio": "7000",
    "royalty": "300000000000000000",
    "fee": "100000000000000000",
    "withdrawFee": "20000000000000000",
    "salt": "0x00000000aff427a68c4fcbe4",
    "conduitKey": "0x1904BFcb93EdC9BF961Eead2e5c0de81dCc1D37D000000000000000000000000",
    "counter": 0
}
```

### 6.4.3 response

```
{
    "code": 200,
    "data": {},
    "msg": "success"
}
```

