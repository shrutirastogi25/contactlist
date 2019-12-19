# contactlist
#include<iostream>
using namespace std;
class contact
{
 public:
 		 char name;
		 int number;
		 contact*next;
		 contact(char a,int n,contact*c=NULL)
		 {
		  name=a;
		  number=n;
		  next=c;
		 }
		 
};
class contactList
{
 contact* head,*tail;
 public:
        contactList()
		{
		 head=tail=NULL;
		}
		bool isempty();
       // contact*createnewcontact(char,int);
		void display();
		void deletion();
		void insert(char,int);
		void addtohead(char,int);
		void addtotail(char,int);
};
void contactList::deletion()
{
 if(head==NULL)
  cout<<"\nThere is no contact in the directory";
 else
 {
  contact*temp,*temp1;
  char del;
  cout<<"\nEnter the name of the contact you wish to delete"<<endl;
  cin>>del;
  if(head->name==del)
  {
   temp1=head;
   head=NULL;
   delete temp1;
  }
  else
  {
   for(temp=head;temp->next->next!=NULL && temp->next->name!=del;temp=temp->next);
   if(temp->next->name==del)
   {
    temp1=temp->next;
	temp->next=temp1->next;
	delete temp1;
   }
   else
    cout<<"\nContact with name "<<del<<" not found in the directory"<<endl;
  }
 }
}
void contactList::insert(char n, int x)
{
 contact* c=new contact(n,x,NULL);
 contact*temp,*temp1;
 if(head==NULL)
   addtohead(n,x);
 else
  if((head->name>=c->name))
   addtohead(n,x);
  else if((tail->name<c->name))
   addtotail(n,x);
  else
  {
   for(temp=head;temp->next->next!=NULL && ((temp->next->name)<=(c->name));temp=temp->next);
   if((temp->next->name)>(c->name))
   {
    c->next=temp->next;
	temp->next=c;
   }
  }
}
void contactList::display()
{
 contact*temp;
 for(temp=head;temp!=NULL;temp=temp->next)
 {
  cout<<"\nName:"<<temp->name<<"\nConatact number: "<<temp->number<<endl;
 }
}
void contactList::addtohead(char n,int x)
{
 contact*c=new contact(n,x,NULL);
 if(head==NULL)
  tail=head=c;
 else
 {
  c->next=head;
  head=c;
 }
}
void contactList::addtotail(char n,int x)
{
 contact*c=new contact(n,x,NULL);
 if(tail==NULL)
  tail=head=c;
 else
 {
  tail->next=c;
  tail=c;
 }
}
int main()
{
 contactList con;
 int add,n,choice;
 char name, ch='y';
 contact* nptr;
 while(ch=='y' || ch=='Y')
 {
  cout<<"\nMAIN MENU"
      <<"\n1.Create new contact"
	  <<"\n2.Delete Contact"
	  <<"\n3.Display all contacts"
	  <<"\nEnter choice(1-3)"<<endl;
  cin>>choice;
  switch(choice)
  {
   case 1:cout<<"\nEnter the name of the contact"<<endl;
          cin>>name;
		  cout<<"\nENter the contact number"<<endl;
		  cin>>n;
		  con.insert(name,n);
		  con.display();
		  break;
   case 2:con.deletion();
          con.display();
		  break;
   case 3:con.display();
          break;
   default:cout<<"\nINVALID CHOICE"<<endl;
           break;
  }
  cout<<"\nDo you wish to continue?(y/n)"<<endl;
  cin>>ch;
 }
 return 0;
}
 
 

   

