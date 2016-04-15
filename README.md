# Big-Data-Analytics
 這個程式使用logstash去twitter抓取關鍵字為Apple的tweet，之後再把資料輸出到elasticsearch 去做儲存，最後再使用elasticsearch-dump把資料匯出成json檔案
 
 * OS: 
    * Ubuntu 14.04 (http://www.ubuntu.com/)
 * Tool: 
    * logstash (https://www.elastic.co/products/logstash)
    * elasticsearch (https://www.elastic.co/products/elasticsearch)
    * elasticsearch-dump (https://github.com/taskrabbit/elasticsearch-dump) 
* Data Sources :
    * Twitter Streaming API (https://apps.twitter.com/)

## logstash
 首先需先取得Twitter Streaming API的KEY，再來撰寫logstash的conf檔，並把要搜尋的關鍵字keyword設定為Apple，取得的資料輸出到elasticsearch中
 ```
 input{
	twitter {
	    consumer_key => "KkiWHXqd3nVDYKBXeKCMvu48Y"     //這四行為twitter API的金鑰
	    consumer_secret => "0ux98sv3pjw2F4ssiNy3H2LelRLoWb5Rq9kQfhLiYGg09aF0E1"
	    oauth_token => "709701184437616640-IxPV5RIllxdDVoAy3ZOZHQkBt8H8TRP"
	    oauth_token_secret => "vmlDxZWbJsSe2yVnUd5tPTBLj9iNz2tFWkDLJnvEUboOm"
	    keywords => ["Apple"]   //搜尋的關鍵字
	    languages => ["en"]     //限制語言為English
	    full_tweet => true      //設定為取得完整tweet
	}
}
output{
	elasticsearch{  
		index => "twitter_apple"    //將資料輸出至elasticsearch，並將資料index儲存為twitter_apple
	}
}
```

## Data Format

```
{
    "_index": "twitter_apple",   //存在elasticsaerch中的哪個資料表
    "_type": "logs",  //資料類型
    "_id": "AVQJgOu4ZPwiXHZYXljN",  // elasticearch 產生的 id
    "_score": 0,
    "_source": {
        "created_at": "Tue Apr 12 08:05:08 +0000 2016",  //建立時間 
        "id": 719798491011088400, //tweets 的 id
        "id_str": "719798491011088384",
        "text": "❤❤15226 Sold- Apple #iPhone5 16GB Factory Unlocked #Smartphone White/Black #iPhone #Deal… https://t.co/SFBfZKl0S7 https://t.co/jugZ6KHTny",   //發文內容        
        "source": "<a href=\"http://dlvr.it\" rel=\"nofollow\">dlvr.it</a>",
        "truncated": false,
        "in_reply_to_status_id": null,
        "in_reply_to_status_id_str": null,
        "in_reply_to_user_id": null,
        "in_reply_to_user_id_str": null,
        "in_reply_to_screen_name": null,
        "user": {  //發文者資料
            "id": 760962086,    //發文者id
            "id_str": "760962086",
            "name": "Unlocked iPhone Sold", //發文者名字 
            "screen_name": "iPhoneUnlocked9",   //發文者帳號名
            "location": "U.S.A.",   //發文者地點
            "url": null,
            "description": "Top 10 #Bestseller, Most Watched/Popular Unlocked #iPhone on eBay Right Now.  #Apple #iPhone5 #iPhone4 #iPhone3 #Onsale #Auction",
            "protected": false,
            "verified": false,
            "followers_count": 940,
            "friends_count": 376,
            "listed_count": 66,
            "favourites_count": 10,
            "statuses_count": 180727,
            "created_at": "Thu Aug 16 06:21:59 +0000 2012",
            "utc_offset": -25200,
            "time_zone": "Pacific Time (US & Canada)",
            "geo_enabled": false,
            "lang": "en",
            "contributors_enabled": false,
            "is_translator": false,
            "profile_background_color": "022330",
            "profile_background_image_url": "http://abs.twimg.com/images/themes/theme15/bg.png",
            "profile_background_image_url_https": "https://abs.twimg.com/images/themes/theme15/bg.png",
            "profile_background_tile": true,
            "profile_link_color": "0000F0",
            "profile_sidebar_border_color": "A8C7F7",
            "profile_sidebar_fill_color": "C0DFEC",
            "profile_text_color": "333333",
            "profile_use_background_image": true,
            "profile_image_url": "http://pbs.twimg.com/profile_images/701301668864925696/auSUL7s8_normal.jpg",
            "profile_image_url_https": "https://pbs.twimg.com/profile_images/701301668864925696/auSUL7s8_normal.jpg",
            "profile_banner_url": "https://pbs.twimg.com/profile_banners/760962086/1456038768",
            "default_profile": false,
            "default_profile_image": false,
            "following": null,
            "follow_request_sent": null,
            "notifications": null
        },
        "geo": null,
        "coordinates": null,
        "place": null,
        "contributors": null,
        "is_quote_status": false,
        "retweet_count": 0,
        "favorite_count": 0,
        "entities": {
            "hashtags": [{
                "text": "iPhone5",
                "indices": [20, 28]
            }, {
                "text": "Smartphone",
                "indices": [51, 62]
            }, {
                "text": "iPhone",
                "indices": [75, 82]
            }, {
                "text": "Deal",
                "indices": [83, 88]
            }],
            "urls": [{
                "url": "https://t.co/SFBfZKl0S7",
                "expanded_url": "http://dlvr.it/L2MFsM",
                "display_url": "dlvr.it/L2MFsM",
                "indices": [90, 113]
            }],
            "user_mentions": [],
            "symbols": [],
            "media": [{
                "id": 719798490881130500,
                "id_str": "719798490881130496",
                "indices": [114, 137],
                "media_url": "http://pbs.twimg.com/media/Cf086e7VAAAZlwr.jpg",
                "media_url_https": "https://pbs.twimg.com/media/Cf086e7VAAAZlwr.jpg",
                "url": "https://t.co/jugZ6KHTny",
                "display_url": "pic.twitter.com/jugZ6KHTny",
                "expanded_url": "http://twitter.com/iPhoneUnlocked9/status/719798491011088384/photo/1",
                "type": "photo",
                "sizes": {
                    "small": {
                        "w": 340,
                        "h": 340,
                        "resize": "fit"
                    },
                    "thumb": {
                        "w": 150,
                        "h": 150,
                        "resize": "crop"
                    },
                    "medium": {
                        "w": 600,
                        "h": 600,
                        "resize": "fit"
                    },
                    "large": {
                        "w": 800,
                        "h": 800,
                        "resize": "fit"
                    }
                }
            }]
        },
        "extended_entities": {
            "media": [{
                "id": 719798490881130500,
                "id_str": "719798490881130496",
                "indices": [114, 137],
                "media_url": "http://pbs.twimg.com/media/Cf086e7VAAAZlwr.jpg",
                "media_url_https": "https://pbs.twimg.com/media/Cf086e7VAAAZlwr.jpg",
                "url": "https://t.co/jugZ6KHTny",
                "display_url": "pic.twitter.com/jugZ6KHTny",
                "expanded_url": "http://twitter.com/iPhoneUnlocked9/status/719798491011088384/photo/1",
                "type": "photo",
                "sizes": {
                    "small": {
                        "w": 340,
                        "h": 340,
                        "resize": "fit"
                    },
                    "thumb": {
                        "w": 150,
                        "h": 150,
                        "resize": "crop"
                    },
                    "medium": {
                        "w": 600,
                        "h": 600,
                        "resize": "fit"
                    },
                    "large": {
                        "w": 800,
                        "h": 800,
                        "resize": "fit"
                    }
                }
            }]
        },
        "favorited": false,
        "retweeted": false,
        "possibly_sensitive": false,
        "filter_level": "low",
        "lang": "en",
        "timestamp_ms": "1460448308123",
        "@version": "1",
        "@timestamp": "2016-04-12T08:05:08.000Z"
    }
}
```