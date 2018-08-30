#include<bits/stdc++.h>
#define MAX_CHILD_NODES 5
using namespace std ;
class node {

    string data , encryptedData , decryptedData ;
    int nodeNumber ;
    string nodeId , refereceNodeID ;
    vector < string > childReferenceId ;
    string genesisReferenceNodeId , hashValue ;

    int key , currentChildNode ;
    node* parent ;
    node* childNodes[MAX_CHILD_NODES] ;


public :
    node() {
        currentChildNode = 0 ;
        for ( int i = 0 ; i < MAX_CHILD_NODES ; i++ ) {
            childNodes[i] = NULL ;
        }
    }
    void generateKey() ;
    void encryptData() ;
    void decryptData() ;

};

void node::generateKey() {
    // Assumption : Global key for all nodes
    key = 3 ;
    return ;
}
void node::encryptData() {
    // Assumption : Only alpha-numberic data
    encryptedData = "" ;
    int n = data.size() ;
    for ( int i = 0 ; i < n ; i++ ) {
        encryptedData.push_back(data[i]-key) ;
    }
}
void node::decryptData() {
    decryptedData = "" ;
    int n = data.size() ;
    for ( int i = 0 ; i < n ; i++ ) {
        decryptedData.push_back ( encryptedData[i]+key ) ;
    }
}

class Tree {
    node* root ;
    void createGenesisNode( node* newNode ) ;
    void createChildNode ( node* parent , node* childNode ) ;
};

void Tree::createGenesisNode( node* newNode ) {
     root = newNode ;
     root->parent = NULL ;
     return ;
}
void Tree::createChildNode ( node* parent , node* childNode ) {
    parent->childNodes[parent->currentChildNode] = childNode ;
    childNode->parent = parent ;
    parent->currentChildNode++ ;
}
