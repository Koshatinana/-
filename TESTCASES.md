{
    "info": {
        "name": "API Tests",
        "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
    },
    "item": [
        {
            "name": "Create Ad",
            "event": [
                {
                    "listen": "test",
                    "script": {
                        "exec": [
                            "pm.test(\"Status code is 200\", function () {",
                            "    pm.response.to.have.status(200);",
                            "});",
                            "",
                            "pm.test(\"Response contains ad ID\", function () {",
                            "    var jsonData = pm.response.json();",
                            "    pm.expect(jsonData.id).to.be.a('string');",
                            "    pm.environment.set(\"adId\", jsonData.id);",
                            "});"
                        ],
                        "type": "text/javascript"
                    }
                }
            ],
            "request": {
                "method": "POST",
                "header": [],
                "body": {
                    "mode": "raw",
                    "raw": "{\n    \"name\": \"Телефон\",\n    \"price\": 85566,\n    \"sellerId\": 291295,\n    \"statistics\": {\n        \"contacts\": 32,\n        \"like\": 35,\n        \"viewCount\": 14\n    }\n}",
                    "options": {
                        "raw": {
                            "language": "json"
                        }
                    }
                },
                "url": {
                    "raw": "https://qa-internship.avito.com/api/1/item",
                    "protocol": "https",
                    "host": [
                        "qa-internship",
                        "avito",
                        "com"
                    ],
                    "path": [
                        "api",
                        "1",
                        "item"
                    ]
                }
            },
            "response": []
        },
        {
            "name": "Get Ad by ID",
            "event": [
                {
                    "listen": "test",
                    "script": {
                        "exec": [
                            "pm.test(\"Status code is 200\", function () {",
                            "    pm.response.to.have.status(200);",
                            "});",
                            "",
                            "pm.test(\"Response contains correct ad data\", function () {",
                            "    var jsonData = pm.response.json();",
                            "    pm.expect(jsonData.name).to.eql(\"Телефон\");",
                            "    pm.expect(jsonData.price).to.eql(85566);",
                            "    pm.expect(jsonData.sellerId).to.eql(291295);",
                            "    pm.expect(jsonData.statistics.contacts).to.eql(32);",
                            "    pm.expect(jsonData.statistics.like).to.eql(35);",
                            "    pm.expect(jsonData.statistics.viewCount).to.eql(14);",
                            "});"
                        ],
                        "type": "text/javascript"
                    }
                }
            ],
            "request": {
                "method": "GET",
                "header": [],
                "url": {
                    "raw": "https://qa-internship.avito.com/api/1/item/{{adId}}",
                    "protocol": "https",
                    "host": [
                        "qa-internship",
                        "avito",
                        "com"
                    ],
                    "path": [
                        "api",
                        "1",
                        "item",
                        "{{adId}}"
                    ]
                }
            },
            "response": []
        },
        {
            "name": "Get Ads by Seller ID",
            "event": [
                {
                    "listen": "test",
                    "script": {
                        "exec": [
                            "pm.test(\"Status code is 200\", function () {",
                            "    pm.response.to.have.status(200);",
                            "});",
                            "",
                            "pm.test(\"Response contains list of ads\", function () {",
                            "    var jsonData = pm.response.json();",
                            "    pm.expect(jsonData).to.be.an('array');",
                            "    pm.expect(jsonData.length).to.be.above(0);",
                            "    jsonData.forEach(function(ad) {",
                            "        pm.expect(ad.sellerId).to.eql(291295);",
                            "    });",
                            "});"
                        ],
                        "type": "text/javascript"
                    }
                }
            ],
            "request": {
                "method": "GET",
                "header": [],
                "url": {
                    "raw": "https://qa-internship.avito.com/api/1/291295/item",
                    "protocol": "https",
                    "host": [
                        "qa-internship",
                        "avito",
                        "com"
                    ],
                    "path": [
                        "api",
                        "1",
                        "item"
                    ],
                    "query": [
                        {
                            "key": "sellerId",
                            "value": "291295"
                        }
                    ]
                }
            },
            "response": []
        },
        {
            "name": "Get Ad with Non-Existent ID",
            "event": [
                {
                    "listen": "test",
                    "script": {
                        "exec": [
                            "pm.test(\"Status code is 404\", function () {",
                            "    pm.response.to.have.status(404);",
                            "});",
                            "",
                            "pm.test(\"Response contains error message\", function () {",
                            "    var jsonData = pm.response.json();",
                            "    pm.expect(jsonData.result.message).to.eql(\"item 42479491-30b4-4ffa-ae98-b08c8395jhd-5 not found\");",
                            "});"
                        ],
                        "type": "text/javascript"
                    }
                }
            ],
            "request": {
                "method": "GET",
                "header": [],
                "url": {
                    "raw": "https://qa-internship.avito.com/api/1/item/42479491-30b4-4ffa-ae98-b08c8395jhd-5",
                    "protocol": "https",
                    "host": [
                        "qa-internship",
                        "avito",
                        "com"
                    ],
                    "path": [
                        "api",
                        "1",
                        "item",
                        "42479491-30b4-4ffa-ae98-b08c8395jhd-5"
                    ]
                }
            },
            "response": []
        }
    ]
}
