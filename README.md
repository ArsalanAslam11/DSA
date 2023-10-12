# DSA
#include<iostream>
using namespace std;

class node{
public:
int data;                            
node* next;                              //initilization

node(int val)
{
	data=val;
	next=NULL;
}		
};


void inTail(node* &head, int val)
{
	node* n=new node(val);
	if(head==NULL)
	{
		head= n;                                        //using this function we add a node on tail side
		return;
	}
	node* temp=head;
	while(temp->next!=NULL)
	{
		temp=temp->next;
	}
	temp->next=n;
}


void inhead(node* &head, int val)
{
	node* n=new node(val);                           //using this function we add a node on head side
	n->next=head;
	head=n;
}



void insert(node* &head, int val, int position)
{
    if (position < 1)
    {
        cout << "You cant put the number less than 1" << endl;
        return;                                                                    //using this we can insert node at given postion by user
    }

    node* newNode = new node(val);

    if (position == 1)
    {
        newNode->next = head;
        head = newNode;
        return;
    }

    node* temp = head;
    int currentPosition = 1;

    while (temp != NULL && currentPosition < position - 1)
    {
        temp = temp->next;
        currentPosition++;
    }

    if (temp == NULL)
    {
        cout << "Position exceeds the length of the linked list." << endl;
        return;
    }

    newNode->next = temp->next;
    temp->next = newNode;
}



void ascending(node* &head)
{
    if (head == nullptr || head->next == nullptr) {
        return; 
    }

    node* sorted = nullptr;                           //using this function we can display node in ascending order
                                                                       
    while (head != nullptr) {
        node* current = head;
        head = head->next;

        if (sorted == nullptr || current->data <= sorted->data) {
          
            current->next = sorted;
            sorted = current;
        } else {
           
            node* temp = sorted;
            while (temp->next != nullptr && current->data > temp->next->data) {
                temp = temp->next;
            }
            
            current->next = temp->next;
            temp->next = current;
        }
    }

    head = sorted; 
}



bool search(node* head, int key){
	node*temp=head;
	while(temp!=NULL){
		if(temp->data==key){                               //using this function we can search a specific node
			return true;
		}
		temp=temp->next;
	}
	return false;
}



void deletion(node* &head, int val){
	node*temp=head;
	while(temp->next->data!=val){
	  temp=temp->next;
	}                                              //using this fuction we can delete a specific node which we want
	node* todelete=temp->next;
	temp->next=temp->next->next;
	
	delete todelete;
}



void display(node* head)
{
	node* temp=head;                              //using this function we can display node after the uper operations
	while(temp!=NULL)
	{
	cout<<temp->data<<" ";
	temp=temp->next;
	}
	cout<<"Last Node"<<endl;}
	


int main(){
	node* head= NULL;
	cout<<"Insert in tail side:  ";
	
	inTail(head,3);                                      //insert node at tail side
	inTail(head ,4);
	display(head);
	
	cout<<"\nInsert in the head side:  ";
	inhead(head,2);
	inhead(head,1);                                     //insert node at head side
	display(head);
	
	cout << "\nInsert at position 3:  ";
    insert(head, 5, 3);                                  //insert a node at position 3
    display(head);
    
    cout << "\nAscending order:  ";
    ascending(head);                                       //All noded in ascending order
    display(head);


     cout<<"\nSearching:  ";                        //Searching a node at position 3
	cout<<search(head,3)<<endl;
	
	cout<<"\nDeletion:  ";                         //Delete a node 2
	deletion(head,2);
	display(head);
	
	return 0;
	
}
