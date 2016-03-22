# GraphQL schema for OPC UA

uses https://github.com/node-opcua/node-opcua to expose an opc ua server as a graphQL schema


## demo

[here](https://ua-ql.herokuapp.com/graphql?query=%7BuaNode(nodeId%3A%22ns%3D2%3Bi%3D10756%22)%20%7B%0A%20%20...%20showNode%0A%20%20references(first%3A10)%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20referenceTypeId%20%7B%0A%20%20%20%20%20%20%20%20%20%20uaNode%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20...%20showNode%20%20%0A%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20typeDefinition%20%7B%0A%20%20%20%20%20%20%20%20%20%20uaNode%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20...%20showNode%0A%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20browseName%20%7B%0A%20%20%20%20%20%20%20%20%20%20name%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20uaNode%20%7B%0A%20%20%20%20%20%20%20%20%20%20...%20showNode%0A%20%20%20%20%20%20%20%20%20%20dataType%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20...%20expandedNodeIdResult%0A%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20dataValue%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20stringValue%0A%20%20%20%20%20%20%20%20%20%20%20%20typedValue%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20...%20on%20MethodParameterTypedArrayValue%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20value%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20name%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A%7D%0A%0Afragment%20loctext%20on%20LocalizedTextResult%20%7B%0A%20%20value%20%7B%0A%20%20%20%20value%20%7B%0A%20%20%20%20%20%20text%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A%0Afragment%20showNode%20on%20UANode%20%7B%0A%20%20displayName%20%7B%0A%20%20%20%20...%20loctext%0A%20%20%7D%20%20%0A%7D%0A%0Afragment%20expandedNodeId%20on%20ExpandedNodeId%20%7B%0A%20%20%20%20uaNode%20%7B%0A%20%20%20%20%20%20...%20showNode%20%20%20%20%0A%20%20%20%20%7D%0A%7D%0A%0Afragment%20expandedNodeIdResult%20on%20ExpandedNodeIdResult%20%7B%0A%20%20value%20%7B%0A%20%20%20%20value%20%7B%0A%20%20%20%20%20%20...%20expandedNodeId%0A%20%20%20%20%7D%0A%20%20%7D%20%20%0A%7D "demo")


## browsing..

opc.tcp://opcua.demo-this.com:51210/UA/SampleServer

## query..
````
{uaNode(nodeId:"ns=2;i=10756") {
  ... showNode
  references(first:10) {
    edges {
      node {
        referenceTypeId {
          uaNode {
            ... showNode  
          }
        }
        typeDefinition {
          uaNode {
            ... showNode
          }
        }
        browseName {
          name
        }
        uaNode {
          ... showNode
          dataType {
            ... expandedNodeIdResult
          }
          dataValue {
            stringValue
            typedValue {
              ... on MethodParameterTypedArrayValue {
                value {
                  name
                }
              }
              
            }
          }
        }
      }
    }
  }
}
}

fragment loctext on LocalizedTextResult {
  value {
    value {
      text
    }
  }
}

fragment showNode on UANode {
  displayName {
    ... loctext
  }  
}

fragment expandedNodeId on ExpandedNodeId {
    uaNode {
      ... showNode    
    }
}

fragment expandedNodeIdResult on ExpandedNodeIdResult {
  value {
    value {
      ... expandedNodeId
    }
  }  
}
````
## result..

````
{
  "data": {
    "uaNode": {
      "displayName": {
        "value": {
          "value": {
            "text": "ScalarMethod1"
          }
        }
      },
      "references": {
        "edges": [
          {
            "node": {
              "referenceTypeId": {
                "uaNode": {
                  "displayName": {
                    "value": {
                      "value": {
                        "text": "HasProperty"
                      }
                    }
                  }
                }
              },
              "typeDefinition": {
                "uaNode": {
                  "displayName": {
                    "value": {
                      "value": {
                        "text": "PropertyType"
                      }
                    }
                  }
                }
              },
              "browseName": {
                "name": "InputArguments"
              },
              "uaNode": {
                "displayName": {
                  "value": {
                    "value": {
                      "text": "InputArguments"
                    }
                  }
                },
                "dataType": {
                  "value": {
                    "value": {
                      "uaNode": {
                        "displayName": {
                          "value": {
                            "value": {
                              "text": "Argument"
                            }
                          }
                        }
                      }
                    }
                  }
                },
                "dataValue": {
                  "stringValue": "{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: BooleanIn\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=1\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: SByteIn\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=2\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: ByteIn\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=3\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: Int16In\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=4\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: UInt16In\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=5\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: Int32In\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=6\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: UInt32In\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=7\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: Int64In\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=8\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: UInt64In\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=9\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: FloatIn\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=10\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: DoubleIn\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=11\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};",
                  "typedValue": {
                    "value": [
                      {
                        "name": "BooleanIn"
                      },
                      {
                        "name": "SByteIn"
                      },
                      {
                        "name": "ByteIn"
                      },
                      {
                        "name": "Int16In"
                      },
                      {
                        "name": "UInt16In"
                      },
                      {
                        "name": "Int32In"
                      },
                      {
                        "name": "UInt32In"
                      },
                      {
                        "name": "Int64In"
                      },
                      {
                        "name": "UInt64In"
                      },
                      {
                        "name": "FloatIn"
                      },
                      {
                        "name": "DoubleIn"
                      }
                    ]
                  }
                }
              }
            }
          },
          {
            "node": {
              "referenceTypeId": {
                "uaNode": {
                  "displayName": {
                    "value": {
                      "value": {
                        "text": "HasProperty"
                      }
                    }
                  }
                }
              },
              "typeDefinition": {
                "uaNode": {
                  "displayName": {
                    "value": {
                      "value": {
                        "text": "PropertyType"
                      }
                    }
                  }
                }
              },
              "browseName": {
                "name": "OutputArguments"
              },
              "uaNode": {
                "displayName": {
                  "value": {
                    "value": {
                      "text": "OutputArguments"
                    }
                  }
                },
                "dataType": {
                  "value": {
                    "value": {
                      "uaNode": {
                        "displayName": {
                          "value": {
                            "value": {
                              "text": "Argument"
                            }
                          }
                        }
                      }
                    }
                  }
                },
                "dataValue": {
                  "stringValue": "{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: BooleanOut\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=1\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: SByteOut\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=2\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: ByteOut\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=3\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: Int16Out\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=4\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: UInt16Out\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=5\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: Int32Out\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=6\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: UInt32Out\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=7\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: Int64Out\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=8\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: UInt64Out\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=9\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: FloatOut\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=10\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};,{\u001b[36m /*Argument*/\u001b[39m\n\u001b[33m name                         \u001b[39m \u001b[36m/* String                           */\u001b[39m: DoubleOut\n\u001b[33m dataType                     \u001b[39m \u001b[36m/* NodeId                           */\u001b[39m: ns=0;i=11\n\u001b[33m valueRank                    \u001b[39m \u001b[36m/* Int32                            */\u001b[39m: -1\n\u001b[33m arrayDimensions              \u001b[39m \u001b[36m/* UInt32                        [] */\u001b[39m: [ ] (l=0)\n\u001b[33m description                  \u001b[39m \u001b[36m/* LocalizedText                    */\u001b[39m: \u001b[32mlocale=null text=null\u001b[39m\n};",
                  "typedValue": {
                    "value": [
                      {
                        "name": "BooleanOut"
                      },
                      {
                        "name": "SByteOut"
                      },
                      {
                        "name": "ByteOut"
                      },
                      {
                        "name": "Int16Out"
                      },
                      {
                        "name": "UInt16Out"
                      },
                      {
                        "name": "Int32Out"
                      },
                      {
                        "name": "UInt32Out"
                      },
                      {
                        "name": "Int64Out"
                      },
                      {
                        "name": "UInt64Out"
                      },
                      {
                        "name": "FloatOut"
                      },
                      {
                        "name": "DoubleOut"
                      }
                    ]
                  }
                }
              }
            }
          },
          {
            "node": {
              "referenceTypeId": {
                "uaNode": {
                  "displayName": {
                    "value": {
                      "value": {
                        "text": "HasTypeDefinition"
                      }
                    }
                  }
                }
              },
              "typeDefinition": {
                "uaNode": {
                  "displayName": {
                    "value": {
                      "value": {
                        "text": "ScalarMethod1"
                      }
                    }
                  }
                }
              },
              "browseName": {
                "name": "ScalarMethod1"
              },
              "uaNode": {
                "displayName": {
                  "value": {
                    "value": {
                      "text": "ScalarMethod1"
                    }
                  }
                },
                "dataType": {
                  "value": null
                },
                "dataValue": {
                  "stringValue": null,
                  "typedValue": null
                }
              }
            }
          },
          {
            "node": {
              "referenceTypeId": {
                "uaNode": {
                  "displayName": {
                    "value": {
                      "value": {
                        "text": "HasComponent"
                      }
                    }
                  }
                }
              },
              "typeDefinition": {
                "uaNode": {
                  "displayName": {
                    "value": {
                      "value": {
                        "text": "MethodTestType"
                      }
                    }
                  }
                }
              },
              "browseName": {
                "name": "MethodTest"
              },
              "uaNode": {
                "displayName": {
                  "value": {
                    "value": {
                      "text": "MethodTest"
                    }
                  }
                },
                "dataType": {
                  "value": null
                },
                "dataValue": {
                  "stringValue": null,
                  "typedValue": null
                }
              }
            }
          }
        ]
      }
    }
  }
}
````
