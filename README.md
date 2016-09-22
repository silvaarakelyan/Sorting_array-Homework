
#include <iostream>
#include <string>
using namespace std;
void selectionSort(int *,int);//as the name of array itself is a pointer
void bubbleSort(int *,int);
void insertionSort(int *,int);
void mergeSort(int *, bool,int,int);
void merge(int *, int,int,int,bool);
void quickSort(int *,int , int,int);
void print(int *,int);

int SIZE; // I declare SIZE as a global variable, which mostly would be usufull in merge and quick
          //sorts  recursion calls
int main(){
    
    int size; //size of array
    int *array;
  
    
    cout<<"HI this program is sorting the array by using 5 sorting algorithms"<<endl;
    cout<<"On console you will see the steps which are done during sorting"<<endl;
    
    cout<<"Input size of array"<<endl;
    cin>>size;
    SIZE=size;

    array=new int[size];
    cout<<"Input the array"<<endl;
    
    for(int i=0; i<size;i++){
        cin>>array[i];
    }
    
    // as the name of array is a pointer, when we pass it to the function, it is already passed by 
    //reference so the changes are done in original array, but as I have 5 sorting algorithms
    // notice that in each function I create a copy of original array and do changes on it
    //besides the quick sort which is already the last function i do changes on original array 
    
    // for each sorting algorithm I ask to the user wheather she wants to sort it in increasing 
    //or in decreasing order
    
    //And user can see the work flow of algorithms
    
    
    selectionSort(array,size); //as the name of array itself is a pointer
    
    bubbleSort(array,size);
    
    insertionSort(array,size);
    
    
    bool flagmerge;
    int *p=new int[size];
    
    for(int i=0;i<size; i++){
        p[i]=array[i];
    }
    
    cout<<"Merge sort"<<endl;
    cout<<"In which order to you want to sort, if in increasing enter 1 if dicreasing enter 0 "<<endl;
    cin>>flagmerge;
    mergeSort(p,flagmerge,0, size-1);

   
    bool flagquick;
    cout<<"Quick Sort"<<endl;
    cout<<"In which order to you want to sort, if in increasing enter 1 if dicreasing enter 0 "<<endl;
    cin>>flagquick;
    quickSort(array, flagquick,0, size-1);
     
}

void print(int *theArray,int size){
    for(int k=0; k<size;k++){
        cout<<theArray[k]<<" ";
    }
     cout<<endl;
}

void selectionSort(int *Array,int size){
    
    int  hold, index;
    int flag;   
    
    cout<<"Selection sort"<<endl;
    cout<<"In which order to you want to sort, if in increasing enter 1 if dicreasing enter 0 "<<endl;
    cin>>flag;
    
    int array[size];
    
    for(int i=0; i<size;i++){
        array[i]=Array[i];
    }
    
    cout<<"The array sorted by selection sort"<<endl;
    
    if(flag==1){
        
        for(int i=size-1; i>=0; i--){
            index=0;
            
            //Find the max of array
            for(int j=0; j<=i; j++){
                if(array[j]>array[index]){
                    index=j; //index of max element
                }  
            }
            
            //swap 
            hold=array[i];
            array[i]=array[index];
            array[index]=hold;
            
            print(array,size);
            }
            
            
        }
    
    
    else if(flag==0){
         for(int i=size-1; i>=0; i--){
            index=0;
            //Find the min of array
            for(int j=0; j<=i; j++){
                if(array[j]<array[index]){
                index=j; //index of the min element
                }  
            }
            
            //swap 
             hold=array[i];
             array[i]=array[index];
             array[index]=hold;
             print(array,size);
        }
    }    
}

void bubbleSort(int *Array,int size){
    
    int  hold;
    int  flag;   
    
    cout<<"Bubble sort"<<endl;
    cout<<"In which order to you want to sort, if in increasing enter 1 if dicreasing enter 0 "<<endl;
    cin>>flag;
    
   
    int array[size];
    
    for(int i=0; i<size;i++){
        array[i]=Array[i];
    }
    
    cout<<"Sorting by bubble sort"<<endl;
    
    if(flag==1){
        
        for(int i=0; i<size; i++){
        
            for(int j=0; j<size-1; j++){
                if(array[j]>array[j+1]){
                    hold=array[j+1];
                    array[j+1]=array[j];
                    array[j]=hold;
                } //after each such for we will see one item boobled :D at the end of array
                
            print(array,size);
            }
            
        }
    }
    

    else if(flag==0){
    
        for(int i=0; i<size; i++){
        
            for(int j=1; j<size-i; j++)
            {
                if(array[j-1]<array[j])
                {
                    hold=array[j-1];
                    array[j-1]=array[j];
                    array[j]=hold;
                }
            print(array,size);
            }
            
        }
    }
        
}


void insertionSort(int *Array,int size){
    
    int  hold,i,j; 
    int flag;   
    
    cout<<"Insertion sort"<<endl;
    cout<<"In which order to you want to sort, if in increasing enter 1 if dicreasing enter 0 "<<endl;
    cin>>flag;

    int array[size];
    
    for(i=0; i<size;i++){
        array[i]=Array[i];
    }
    
    cout<<"Sorted by insertion sort"<<endl;
    
    if(flag==1){
            
        for( i=0; i<size; i++)
        {
            for(j=i; j>=0; j--)
            {
                if(array[j]<array[j-1])
                {
                    hold=array[j];
                    array[j]=array[j-1];
                    array[j-1]=hold;
                }
            }
            print(array,size);
        }
    }
    
    else if(flag==0){
    
        for(  i=1; i<size; i++){
            
            int  key=array[i];
            for(  j=i-1; ((j>=0)&&(array[j]<key)); j--)
            {
                array[j+1]=array[j];
            }
                array[j+1]=key;
                print(array,size);
        }
    }

        
}
    
void mergeSort(int * Array, bool flag, int first, int last){
    int size=last+1;
    cout<<"Splitting"<<endl;
    print(Array,size);
    if(first<last){
        int mid=(first+last)/2;
        mergeSort(Array,flag, first, mid);
        mergeSort(Array,flag, mid+1, last);
        merge(Array,first, mid, last,flag);
    }

}
const int MAX=999;
void merge(int *Array, int first, int mid, int last,bool flag){
    
    int size=last+1;
    int ArrayTemp[MAX]; //temproorary array
    int first1= first;  //begining of 1st array
    int last1=mid;      //end of 1st array
    int first2=mid+1;   //beginning of 2nd array
    int last2=last;     //end of 2nd array
    
    int index=first1;   //next available location in ArrayTemp
    
    if(flag==1){
        
        while((first1<=last1)&&(first2<=last2)){
       
            if(Array[first1]<Array[first2]){
                ArrayTemp[index]=Array[first1];
                ++first1;
                
            }
        
            else 
            {
                ArrayTemp[index]=Array[first2];
                ++first2;
            }
        
            ++index;
         }
    
      
        while(first1<=last1){
            ArrayTemp[index]=Array[first1];
            ++first1;
            ++index;
        }
    
        while(first2<=last2){
            ArrayTemp[index]=Array[first2];
            ++first2;
            ++index;
        }
        cout<<"Merging"<<endl;
        print(ArrayTemp,size);
        
        for(int i=0; i<=last;i++)
        {
            Array[i]=ArrayTemp[i];
        }
       
    } 
    
    
    else if(flag==0)
    {
     
    
        while((first1<=last1)&&(first2<=last2)){
        
            if(Array[first1]>Array[first2]){
                ArrayTemp[index]=Array[first1];
                ++first1;
            }
        
            else 
            {
            ArrayTemp[index]=Array[first2];
            ++first2;
            }
        
        ++index;
        }
    
      
        while(first1<=last1){
        ArrayTemp[index]=Array[first1];
        ++first1;
        ++index;
        }
    
        while(first2<=last2){
        ArrayTemp[index]=Array[first2];
        ++first2;
        ++index;
        }
    
        cout<<"Merging"<<endl;
        print(ArrayTemp,size);
        
        for(int i=0; i<=last;i++)
        {
        Array[i]=ArrayTemp[i];
        }
     
    }
  
   
}

void quickSort(int *array,int flag, int left, int right) {
      int i = left, j = right;
      int hold;
      int pivot = array[(left + right) / 2];
 
     if(flag==1){
      /*here I do  partition */
      while (i <= j) {
            while (array[i] < pivot)
                  i++;
            while (array[j] > pivot)
                  j--;
            if (i <= j) {
                  hold = array[i];
                  array[i] = array[j];
                  array[j] = hold;
                  i++;
                  j--;
            }
          print(array,SIZE);  
        }
     }
     
     else if(flag==0){
       while (i <= j) {
            while (array[i] > pivot)
                  i++;
            while (array[j] < pivot)
                  j--;
                
             if (i<=j){
                  hold = array[i];
                  array[i] = array[j];
                  array[j] = hold;
                  i++;
                  j--;
                  print(array,SIZE);
            }
            
        }
        print(array,SIZE);
     }
        
     
 
      /* recursion */
      if (left < j){
            quickSort(array,flag, left, j);}
      if (i < right){
            quickSort(array, flag, i, right);}
      
            
}























