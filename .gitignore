//-----------------------------------------------------------------
//  Задание Калькулятор для работы с двоичным представлением чисел
//  Автор:<Карпенко Денис Константинович>
//  Среда разработки:Xcode Version 4.5.2 (4G2008a)
//  Дата последнего изменения20.11.12.
//-----------------------------------------------------------------


#include <iostream>
#include "cmath"
#include "locale"
#include "iomanip"
#include "fstream"
using namespace std;
void InversionBits(int *mass,int NumberofBits);
//команда инвертирования бит
void RightShift(int *mass,int NumberofBits);
//команда правый сдвиг
void MovementBits(int *mass,int NumberofBits);
// команда перемещение цеопчки бит
void ChangeSomeBits(int *mass,int NumberofBits);
//команда изменения отдельных бит
void LeftShift(int *mass,int NumberofBits);
//команда левый сдвиг
void RealDecBin(int*mass, float number,int const Category);
// команда перевод вещественного числа в двоичный код
void ChangesChainBits(int *mass,int NumberofBits);
//команда обмена цеопочек бит
void BinDec(int* bin, int size);
// команда перевода из двоичного кода в десятичный (целые числа)
void RealBinToDec(int*mass,int const category);
//перевод вещественых чисел из двоичного в дестичное представление
void RealChangeBits(int*mass,int const Category);
//изменение бит вещественного числа
void RealDigits(ofstream & fout);
//подпрограмма которая содержит все функции для вещественных чисел
void translateInto2(int *mass,double a,int NumberofBits);
//перевод целого числа из десятичного в двоичный код
void NaturalDigits(ofstream &fout);
//подпрограмма которая содержит все функции для целых чисел

int main(int argc, const char * argv[]){
    setlocale(LC_ALL, "russian");
    double MenuNumber;
    bool run=1;
    string path;
    cout<<"Добро пожаловать в калькулятор для работы с двоичным представлением числа\n";
    cout<<"Введите путь файла для хранения результатов\n>";
    cin>>path;
    ofstream fout(path);
    while(run){
        cout<<"1)вещественные числа\n";
        cout<<"2)целые числа\n";
        cout<<"3)конец программы\n> ";
        cin>>MenuNumber;
        if(MenuNumber==1)
            RealDigits(fout);
        if (MenuNumber==2)
            NaturalDigits(fout);
        if(MenuNumber==3)
            run=0;
    }
}


void NaturalDigits(ofstream & fout){
    int MenuNumber;
    bool correct=1,stop=1,newnumber=1,correct2=1;
    long double UserNumber;
    int NumberofBits;
    
    while (correct) {
        //цикл проверки верного ввода кол-ва разрядов
        while(correct2){
            cout<<"\nвведите кол-во разрядов(8 ,16, или 32)\n> ";
            cin>>NumberofBits;
            if((NumberofBits==8)||(NumberofBits==16)||(NumberofBits==32))
                correct2=0;
        }
        if(correct2==0){
            cout<<"введите число\n> ";
            cin>>UserNumber;
            if(UserNumber>floor(UserNumber))
                cout<<"\nВы ввели вещественное число,программа будет работать с целой частью\n";
            if(abs(UserNumber)>pow(2.,NumberofBits))
                cout<<"\nВы ввели слишком большое число ,некоторые биты будут отрезаны\n";
        }
        fout<<UserNumber<<"\n";
        int mass[33]={};
        newnumber=0;
        stop=1;
        translateInto2(mass,UserNumber,NumberofBits);
        for(int i=NumberofBits;i>=1;i--){
            //вывод массива с конца
            fout<<mass[i];
        }
        fout<<"\n";
        fout.flush();
        while(stop){
            //запуск меню после каждой используемой функции
            cout<<"\n"<<setw(20)<<"Меню";
            cout<<"\n  выберите операцию:\n";
            cout<<"1)изменить некоторые биты\n";
            cout<<"2)сделать инверсию бит\n";
            cout<<"3)перемещение последовательности бит на указанную позицию\n";
            cout<<"4)перестановка цепочек бит\n";
            cout<<"5)левый сдвиг на указанное кол-во бит\n";
            cout<<"6)правый сдвиг на указанное кол-во бит\n";
            cout<<"7)показать 10ный эквивалент\n";
            cout<<"8)вернуться к выбору числа и кол-ва разрядов\n";
            cout<<"9)Вернуться к выбору вида числа\n> ";
            cin>>MenuNumber;
            if(MenuNumber==1)
                ChangeSomeBits(mass,NumberofBits);
            if(MenuNumber==2)
                InversionBits(mass,NumberofBits);
            if(MenuNumber==3)
                MovementBits(mass,NumberofBits);
            if(MenuNumber==4)
                ChangesChainBits(mass,NumberofBits);
            if(MenuNumber==5)
                LeftShift(mass,NumberofBits);
            if(MenuNumber==6)
                RightShift(mass,NumberofBits);
            if(MenuNumber==7)
                BinDec(mass,NumberofBits);
            if(MenuNumber==8){
                //параметр выхода из главного меню
                correct=1;
                correct2=1;
                stop=0;
            }
            if(MenuNumber==9){
                //параметр выхода из всех циклов
                stop=0;
                correct=0;
            }
            for(int i=NumberofBits;i>=1;i--){
                //вывод массива с конца
                fout<<mass[i];
            }
            fout<<"\n";
            fout.flush();
        }
    }
    
}
void translateInto2(int *mass,double a,int NumberofBits){
    //перевод десятичного числа в двоичную
    bool have=1;
    unsigned int x;
    long double NewDigit=1;
    int i;
    int const sistem=2;
    for(i=0;i<NumberofBits;i++){
        //нахождение двойки в степени(кол-ва разрядов)
        NewDigit*=2;
    }
    a=floor((a));
    int numel=0;
    x=a;
    i=1;
    if(a<0)
        x=NewDigit+a;
    while(have){
        // перевод в симеричную систему
        mass[i]=x%sistem;
        // массиву присаваиваются остатки
        x/=sistem;
        // число делится остатки откидываются(целочисленое деление)
        i++;
        numel++;
        if(x==0){
            have=0;  }}
    //параметр конца цикла
    
    cout<<"Двоичный код=";
    for(i=NumberofBits;i>=1;i--){
        //вывод массива с конца
        cout<<mass[i];
    }
}

void ChangeSomeBits(int *mass,int NumberofBits){
    //изменение значений некоторых бит
    int changesBits;
    int i;
    int quantity;
    cout<<"\nвведите количество изменяемых бит\n>";
    cin>>quantity;
    for(i=0;i<quantity;i++){
        bool correct=1;
        while(correct){
            cout<<"введите номер изменяемого бита(нумерация справа)\n> ";
            cin>>changesBits;
            if(changesBits>0&&changesBits<NumberofBits)
                correct=0;
        }
        if (mass[changesBits]==0)
            //если значение было равно 0 то ему присваивается значение  1
            mass[changesBits]=1;
        else{
            mass[changesBits]=0;
            // если было равно 1 то присваивается 0
        }
    }
    for(i=NumberofBits;i>=1;i--){
        //вывод массива с конца
        cout<<mass[i];
        
    }
}


void InversionBits(int *mass,int NumberofBits){
    //инверсия бит
    int i;
    for(i=NumberofBits;i>0;i--){
        // для каждого элменета массива происходит замена значения 0->1 и 1->0
        if(mass[i]==0)
            mass[i]=1;
        else{
            mass[i]=0;
        }
    }
    for(i=NumberofBits;i>=1;i--)
        //вывод массива с конца
        cout<<mass[i];
}

void MovementBits(int *mass,int NumberofBits){
    //копирование цепочки бит
    int quantity;
    int StartPosition;
    int SecondPosition;
    int i;
    cout<<"\nВведите количество перемещаемых бит\n> ";
    cin>>quantity;
    cout<<"\nВведите начальную позицию цепочки(нумерация справа)\n> ";
    cin>>StartPosition;
    cout<<"\nВведите конечную позицию цепочки(нумерация справа)\n> ";
    cin>>SecondPosition;
    for(i=0;i<quantity;i++){
        mass[SecondPosition+i]=mass[StartPosition+i];
        //присвоение конечной позиции значения соответсвующих элементов
    }
    for(i=NumberofBits;i>=1;i--)
        //вывод массива с конца
        cout<<mass[i];
}

void ChangesChainBits(int *mass,int NumberofBits){
    //обмен цепочек бит
    int quantity;
    int FirstChain;
    int i;
    int SecondChain;
    cout<<"\nВведите размер перемещаемых цепочек\n> ";
    cin>>quantity;
    cout<<"\nВведите начало первой цепочки(нумерация справа)\n> ";
    cin>>FirstChain;
    cout<<"\nВведите начало второй цепочки(нумерация справа)\n> ";
    cin>>SecondChain;
    if(quantity>SecondChain-FirstChain){
        cout<<"\nцепочки битов пересекаются!!\n";
    }
    else{
        for(i=0;i<quantity;i++)
            swap(mass[FirstChain+i],mass[SecondChain+i]);
        //обмен значений элементов цепочек
    }
    for(i=NumberofBits;i>=1;i--){
        // вывод массива с конца
        cout<<mass[i];
    }
    
    
}

void LeftShift(int *mass,int NumberofBits){
    //левый сдвиг
    int ShiftLenght;
    int i;
    cout<<"\nВведите количество бит на которые будет произведен сдвиг\n> ";
    cin>>ShiftLenght;
    if(ShiftLenght>NumberofBits){
        //если сдвиг больше кол-ва разрядов то все элементы равны 0
        for(i=0;i<NumberofBits;i++)
            mass[i]=0;
    }
    else{
        
        for(i=NumberofBits;i>ShiftLenght;i--)
            mass[i]=mass[i-ShiftLenght];
        for(i=0;i<=ShiftLenght;i++) 
            mass[i]=0;
    }
    for(i=NumberofBits;i>=1;i--)
        cout<<mass[i];
}

void RightShift(int *mass,int NumberofBits){
    //правый сдвиг
    int ShiftLenght;
    int SignedNumber;
    int i;
    cout<<"\nВведите количество бит на который будет произведен сдвиг\n";
    cin>>ShiftLenght;
    SignedNumber=mass[NumberofBits];
    for(i=0;i<(NumberofBits-ShiftLenght);i++)
        mass[i]=mass[i+ShiftLenght];
    for(i=NumberofBits;i>=(NumberofBits-ShiftLenght);i--)
        //старший бит был равен одному то слева выдвигаются единицы(арифметический сдвиг)
        mass[i]=SignedNumber;
    for(i=NumberofBits;i>=1;i--)
        cout<<mass[i];
}

void BinDec(int* mass, int size){
    //перевод в десятичную
    int NewDigit=1;
    int Signed;
    int sum=0, i;
    cout<<"\n Если число со знаком нажмите 1\n> ";
    cin>>Signed;
    cout<<"\nДесятичное число:\n< ";
    for(i=0;i<=(size); i++)
        sum+=mass[i]*pow(2.,i-1);
    for(i=1;i<=size;i++){
        NewDigit*=2;
    }
    if((Signed==1)&&(mass[size]==1))
        // пользователь выбрал знаковое и число отрицательное
        cout<<sum-NewDigit;
    else{
        cout<<sum;
    }
}

void RealDigits(ofstream & fout){
    float UserNumbers;
    int const Category=32;
    bool correct=1;
    int MenuNumber=0;
    cout<<"Введите число\n> ";
    cin>>UserNumbers;
    fout<<UserNumbers<<"\n";
    //вывод в файл
    int mass[Category]={};
    if(UserNumbers!=0)
        RealDecBin(mass,UserNumbers,Category);
    for(int i=0;i<Category;i++){
        //вывод массива
        fout<<mass[i];
    }
    fout<<"\n";
    fout.flush();
    while(correct){
        cout<<"\n1)перевод в десятичное число\n";
        cout<<"2)Изменить биты\n";
        cout<<"3)вернуться к выбору вида числа\n> ";
        cin>>MenuNumber;
        if(MenuNumber==1)
            RealBinToDec(mass,Category);
        if(MenuNumber==2)
            RealChangeBits(mass,Category);
        if (MenuNumber==3)
            correct=0;
        
    }
}

void RealDecBin(int*mass, float x,int const Category){
    //перевод в двоичный код
    char*p=(char*)(&x);
    //указатель на один байт числа
    int i,a;
    char y=1;
    for(i=0;i<4;i++){
        //цикл для считывания 4 байтов
        for(a=0;a<8;a++){
            //цикл для  считывания элементов одного байта и заполение в массив
            
            if(((*p)&y)==0){
                //побитовое "и" помогает нам узнать 1или0 стоит в данном бите
                mass[31-a-i*8]=0;
                
            }
            else{
                mass[31-a-i*8]=1;
            }
            y=y <<1;
        }
        p=p+1;
        y=1;
        
    }
    for(i=0;i<Category;i++)
        // вывод массива
        cout<<mass[i];
    
}


void RealChangeBits(int*mass,int const Category){
    int changesBits;
    int i;
    int quantity;
    cout<<"\nвведите количество изменяемых бит\n>";
    cin>>quantity;
    for(i=0;i<quantity;i++){
        cout<<"введите номер изменяемого бита\n> ";
        cin>>changesBits;
        if (mass[changesBits-1]==0)
            //если значение было равно 0 то ему присваивается значение  1
            mass[changesBits-1]=1;
        else{
            mass[changesBits-1]=0;
            // если было равно 1 то присваивается 0
        }
    }
    for(i=0;i<Category;i++)
    {
        //вывод массива
        cout<<mass[i];
        
    }
}

void RealBinToDec(int*mass,int const category){
    int Exp=0;
    int IntegralPart=0;
    float RealPart=0;
    int i;
    int SignedNumber;
    int degree=1;
    if(mass[0]==1){
        SignedNumber=-1;
        //нахождение знака числа
    }
    else{
        SignedNumber=1;
    }
    for(i=8;i>=1;i--){
        //перевод экспоненты в десятичное число
        Exp+=mass[i]*degree;
        degree*=2;
        
    }
    Exp-=127;
    degree=1;
    if(Exp>=0){
        //нахождение десятичного эквивалента целой части
        for(i=8+Exp;i>=9;i--){
            IntegralPart+=mass[i]*degree;
            degree*=2;
        }
        
        IntegralPart+=degree;
        
        degree=1;
        for(i=category;i>=9+Exp;i--){
            //нахождение десятичного эквивалента дробной части
            if(mass[i]==1)
                RealPart=1+RealPart/2;
            if(mass[i]==0)
                RealPart=RealPart/2;
            
        }
        RealPart/=2;
        cout<<"\n"<<SignedNumber*(RealPart+IntegralPart);
    }
    else{
        for(i=category;i>=9;i--){
            if(mass[i]==1)
                RealPart=1+RealPart/2;
            if(mass[i]==0)
                RealPart=RealPart/2;
            
        }
        RealPart=1+RealPart/2;
        //так как единица отбрасывается
        for(i=Exp;i<0;i++){
            RealPart/=2;
        }
        cout<<"\n"<<RealPart*SignedNumber;
    }
}
    
