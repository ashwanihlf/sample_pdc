# Hyperledger Fabric network setup for exploring Private data Collection

Pre Requisite - Hyperledger Binaries and HLF Pre-Requisites software are installed

# Following are the steps to run the setup
1. create a working folder, change directory to working folder
2. git clone https://github.com/ashwanihlf/sample_pdc.git
3. sudo chmod -R 755 sample_pdc/
4. cd sample_pdc  
5. mkdir config  
	<remove config and crypto-config if they are existing before creation of config folder (Optional)>
	5a. sudo rm -rf config
	5b  sudo rm -rf crypto-config
6. export COMPOSE_PROJECT_NAME=net
7. sudo ./generate.sh
8. sudo ./start.sh
9. docker exec -it cli /bin/bash
10. peer chaincode invoke -C mychannel -n samplecc -c '{"function":"initCar","Args":["Ashwani","Blue","BMW"]}'
11. peer chaincode query -C mychannel -n samplecc -c '{"function":"readCar","Args":["Ashwani"]}'      

>> returns {"color":"bmw","docType":"Car","model":"blue","owner":"Ashwani"}

12. peer chaincode query -C mychannel -n samplecc -c '{"function":"carPrice","Args":["Ashwani"]}'      

>> returns {"docType":"CarPrice","owner":"Ashwani","price":3000}


13. export CORE_PEER_LOCALMSPID="Org2MSP"
14. export CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp
15. export CORE_PEER_ADDRESS=peer0.org2.example.com:7051
16. 8. peer chaincode query -C mychannel -n samplecc -c '{"function":"readCar","Args":["Ashwani"]}' 

>> returns {"docType":"Car","owner":"Ashwani","color":"blue","model":"bmw"}

17.  peer chaincode query -C mychannel -n samplecc -c '{"function":"carPrice","Args":["Ashwani"]}'  

>> message:"{\"Error\":\"Failed to get state for Ashwani: GET_STATE failed: transaction ID: e6e4c03f480f1199b51813f3b162c3c98691616b5965ba3c79f8e5af5643b606: 
 tx creator does not have read access permission on privatedata in chaincodeName:samplecc collectionName: collectionPrivate\"}"
