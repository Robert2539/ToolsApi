pipeline{
agent any
stages{

stage('test'){
steps{
script {
newman run ToolsRental.postman_collection.json -g workspace.postman_globals.json --reporters html
 
}
}
}

}

}