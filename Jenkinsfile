pipeline{
agent any
stages{

stage('test'){
steps{
script {
cd C:\Users\pricx\Downloads\ToolsAPIjson
newman run ToolsRental.postman_collection.json -g workspace.postman_globals.json --reporters html
 
}
}
}

}

}