# Practice
practice
#include<iostream>
using namespace std;
#define MaxSize 50

typedef struct {
    char data[MaxSize];
    int length;
}SqString;

void GetNext(SqString t, int next[]) {
    int j, k;
    j = 0, k = -1;
    next[0] = -1;
    while (j < t.length - 1) {
        if (k == -1 || next[k] == next[j]) {
            j++, k++;
            next[j] = k;
        }
        else k = next[k];
    }
}

int KmpIndex(SqString s, SqString t) {
    int next[MaxSize], i = 0, j = 0;
    GetNext(t, next);
    while (i < s.length && j < t.length) {
        if (j == -1 || s.data[i] == t.data[j]) {
            j++, i++;
        }
        else j = next[j];
    }
    if (j >= t.length) {
        return i - t.length;
    }
    else return -1;
}

void GetNextval(SqString t, int Nextval[]) {
    int j = 0, k = -1;
    Nextval[0] = -1;
    while (j < t.length) {
        if (k == -1 || t.data[j] == t.data[k]) {
            j++, k++;
            if (t.data[j] != t.data[k]) {
                Nextval[j] = k;
            }
            else Nextval[j] = Nextval[k];
        }
        else k = Nextval[k];
   }
}

int KmpIndexl(SqString s, SqString t) {
    int Nextval[MaxSize], i = 0, j = 0;
    GetNextval(t, Nextval);
    while (i < s.length && j < t.length) {
        if (j == -1||s.data[i] == t.data[j]) {
            i++, j++;
        }
        else j = Nextval[j];
    }
    if (j >= t.length) {
        return i - t.length;
    }
    else return -1;
}

int KmpIndexlcount(SqString s, SqString t) {//计算子串在父串中不重叠出现次数
    int Nextval[MaxSize], i = 0, j = 0, count = 0;
    GetNextval(t, Nextval);
    while (i < s.length && j < t.length) {
        if (j == -1 || s.data[i] == t.data[j]) {
            i++, j++;
        }
        else j = Nextval[j];

        if (j >= t.length) {
            count++;
            j = 0;
        }
    }
        return count;
}

int main() {
    SqString a, b;
    cin >> a.data >> b.data;
    cin >> a.length >> b.length;
    //cout << KmpIndex(a, b);
    //cout << KmpIndexl(a, b);
    cout << KmpIndexlcount(a, b);
    return 0;
}
