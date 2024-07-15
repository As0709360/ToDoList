#include<iostream>
#include<vector>
#include<stdlib.h>
#include<string>
#include<fstream>

using namespace std;

class ToDoList{
	private:
		vector<string> tasks;
		  vector<string> temp;
	public:
        
		void addtask();
		void showtask();
		void deletetask();
		void exitcode();
		void defalutcode();
		void marktask();
		void index();
	
};

int TaskNo = 0;
	void ToDoList::addtask(){
		system("cls");
	 	cout << "\n\t\tEnter new task here : ";
		string task;
		cin.ignore();
		getline(cin, task);
		char save;
		cout<<"\n\t\tWould you like to save task -(y/n)"; 
		cin>>save;           
		if(save == 'y'){
		ofstream fout;
		fout.open("todofile", ios::app);				
		fout << task << endl;
		TaskNo++;
		fout.close();
		cout<<"\n\t\tTask Added Successfully!" << endl;
	}
	else{
		cout<<"\n\t\tTask not Saved in List "<<endl;
		return;
	}
}
	
	void ToDoList::showtask(){
		system("cls");
		ifstream fin("todofile");
		if (!fin) {   //checking for file, exist or not
		cout << "\nNo tasks to display" << endl;
		return;   
		}
		string task;
		TaskNo = 1 ;
		cout << "\t\t------ All Tasks ------" << endl;
		while(getline(fin, task)){
			cout <<"\n\t\t"<< TaskNo << ". " << task << endl; 
		TaskNo++;
		}
		fin.close(); //for colsing the file
}

	void ToDoList::deletetask(){
  		system("cls");
    	ifstream fin("todofile");
    	if (!fin) {   //checking file exist or not
        cout << "\nNo tasks to delete" << endl;
			return; 
		}
	vector<string> temp;
		string task;
		int count = 1;
		while(getline(fin, task)){
			temp.push_back(task);
			count++;
		}
		fin.close();
		if(count == 1){
			cout<<"\n\t\tNo tasks exist to delete."<<endl;
			return;
		}
		cout<<"\n\t\tEnter task number to delete:";
		int taskno;
		cin>>taskno;
		if(taskno <1 ||taskno >= count){
			cout<<"\n\t\tInvalid task number."<<"\n";
		}
		else{
        temp.erase(temp.begin()+(taskno-1));
        cout << "\n\t\tTask Deleted Successfully!" << endl;      
        ofstream fout;
        fout.open("todofile", ios::out | ios::trunc);
        for(int i = 0; i < temp.size(); i++){
            fout << temp[i] << endl;
        }
        fout.close();
     }
}
		
	void ToDoList::marktask(){
		system("cls");
		ifstream fin("todofile");
		if (!fin) {   
			cout << "\nNo tasks to mark as Completed or Not" << endl;
			return;  
		}
		vector<string> temp;
		string task;
		int count = 1;
		while(getline(fin, task)){
			temp.push_back(task);
			count++;
		}
		fin.close();
		if(count == 1){
			cout<<"\n\t\tNo tasks exist to mark as Completed or Not."<<endl;
			return;
		}
		cout<<"\n\t\tEnter task number to mark as Completed or Not : ";
		int taskno;
		cin>>taskno;
		if(taskno <1 ||taskno >= count){
			cout<<"\n\t\tInvalid task number."<<"\n";
		}
		else{
			char marks;
			cout<<"\n\t\tMark task as 'Completed or Not' ? (y/n)- ";
			cin>>marks;
			if(marks=='y' || marks == 'Y') {

				temp[taskno - 1] += " - Completed";
			cout << "\n\t\tTask marked as completed successfully." << endl;
		} else {
			temp[taskno - 1] += " - Pending";
			cout << "\n\t\tTask marked as not completed." << endl;
		}

		ofstream fout("todofile", ios::out | ios::trunc);
		for (const auto &line : temp) {
			fout << line << endl;
		}
		fout.close();
		}
	}

	void ToDoList::exitcode(){
		system("cls");
		char ex;
		
		cout<<"\n\t\tWould you like to exit ? - (y/n)";
		cin>>ex;
		if(ex == 'y'){
			system("cls");
			cout<<"\n\t\t_______________________________________";
			cout<<"\n\t\t   THANKS FOR VISIT, Have A GoodDay!  ";
			cout<<"\n\t\t_______________________________________";
			cout<<"\n";
			cout<<"\n";
			cout<<"\n";
			exit(0);
		}
		if(ex != 'y'){
			cout<<"Task Not Saved "; 
			system("cls") ;	
		}
	}

	void ToDoList::defalutcode(){
				system("cls");
			cout<<"\n\t\t_______________________";
			cout<<"\n\t\t\tERROR....";
			cout<<"\n\t\t_______________________";
			cout<<"\n\n\tYou have pressed the wrong option, please enter the correct one. "<<endl;
			cout<<endl;
			
	}

		
	void ToDoList::index(){
		system("cls");
		cout<<"\n\t\t______________________________________";
		cout<<"\n\t\t             To-Do List  ";
		cout<<"\n\t\t______________________________________";
	}

int main(){

	ToDoList todo;
	todo.index();
	int choice;
	
	do{
		cout<<"\n\t\tEnter 1. For Adding new Task in list";
		cout<<"\n\t\tEnter 2. For Veiw all Task from list";
		cout<<"\n\t\tEnter 3. For Delete task from list";
		cout<<"\n\t\tEnter 4. For Mark the task (Completed or Not)";
		cout<<"\n\t\tEnter 5. For Exit from ToDo-List";
		cout<<"\n\t\tEnter Your Choice here-";
		cin>>choice;
	
		switch(choice){
			case 1:
				todo.index();
				todo.addtask();
				break;
			
			case 2:
				todo.index();
				todo.showtask();
				break;
				
			case 3:
				todo.index();
				todo.deletetask();
				break;
				
			case 4:
				todo.index();
				todo.marktask();
				break;
				
			case 5:
				todo.exitcode();
				
			default:
				todo.defalutcode();
				break;	
		}
	}while(1);	
}
