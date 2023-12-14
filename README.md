# job-queue-dsl
//Job Queue
#include <iostream>
#define MAX 10

using namespace std;

struct queue {
    int data[MAX];
    int front, rear;
};

class Queue {
    struct queue q;

public:
    Queue() {
        q.front = q.rear = -1;
    }
    int isempty();
    int isfull();
    void enqueue(int);
    int delqueue();
    void display();
};

int Queue::isempty() {
    return (q.front == -1 || q.front > q.rear) ? 1 : 0;
}

int Queue::isfull() {
    return (q.rear == MAX - 1) ? 1 : 0;
}

void Queue::enqueue(int x) {
    if (isfull()) {
        cout << "Queue is overflow!!!" << endl;
    }
    else {
        if (q.front == -1)
            q.front = 0;
        q.data[++q.rear] = x;
    }
}

int Queue::delqueue() {
    if (isempty()) {
        cout << "Queue is underflow!!!" << endl;
        return -1;
    }
    else {
        int x = q.data[q.front++];
        return x;
    }
}

void Queue::display() {
    if (isempty()) {
        cout << "Queue is empty!!!" << endl;
    }
    else {
        cout << "Queue contains : ";
        for (int i = q.front; i <= q.rear; i++) {
            cout << q.data[i] << " ";
        }
        cout << endl;
    }
}

int main() {
    Queue obj;
    int ch, x;
    do {
        cout << "\n1. Insert Job\n2. Delete Job\n3. Display\n4. Exit\nEnter your choice: ";
        cin >> ch;
        switch (ch) {
        case 1:
            cout << "\nEnter data: ";
            cin >> x;
            obj.enqueue(x);
            break;
        case 2:
            x = obj.delqueue();
            if (x != -1) {
                cout << "\nDeleted Element = " << x << endl;
            }
            break;
        case 3:
            obj.display();
            break;
        case 4:
            cout << "\nExiting Program.....\n";
            break;
        default:
            cout << "\nInvalid Choice!!!\n";
            break;
        }
    } while (ch != 4);
    return 0;
}


