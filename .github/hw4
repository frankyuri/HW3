#include <iostream>
using namespace std;
#define MAX_TERMS 10 
typedef struct {
	int coef;
	int expo;
} polynomialTerm;
typedef struct linkedTerm {
	int coef;
	int expo;
	linkedTerm* nextTermPtr;
} linkedPolynomialTerm;
void clear(polynomialTerm t[])
{
	for (int i = 0; i < MAX_TERMS; i++) {
		t[i].coef = 0;
		t[i].expo = 0;
	}
	return;
}
void clear(linkedPolynomialTerm*& polynomialTermPtr)
{
	linkedPolynomialTerm* tmpPtr;

	while (polynomialTermPtr != nullptr) {
		tmpPtr = polynomialTermPtr;
		polynomialTermPtr = polynomialTermPtr->nextTermPtr;
		delete tmpPtr;
	}
}
void inputTerms(polynomialTerm t[], int co, int ex)
{
	for (int i = 0; i < MAX_TERMS; i++) {
		if (ex == t[i].expo) {
			t[i].coef = co;
			break;
		}
		if (ex > t[i].expo) {
			for (int j = MAX_TERMS; j >= i; j--) {
				t[j] = t[j - 1];
			}
			t[i].expo = ex;
			t[i].coef = co;
			break;
		}
	}
	return;
}
void inputLinkTerms(linkedPolynomialTerm*& polyPtr, int coef, int expo)////
{
	linkedPolynomialTerm* tmpPtr;

	tmpPtr = new linkedPolynomialTerm;
	tmpPtr->coef = coef;
	tmpPtr->expo = expo;

	if (!polyPtr || polyPtr->expo <= expo) {  
		if (polyPtr && polyPtr->expo == expo)  
			tmpPtr->nextTermPtr = polyPtr->nextTermPtr;
		else
			tmpPtr->nextTermPtr = polyPtr;
		polyPtr = tmpPtr;
	}
	else {
		linkedPolynomialTerm* tmp = polyPtr;
		while (true) {
			if (tmp->nextTermPtr && tmp->nextTermPtr->expo <= expo) {  
				if (tmp->nextTermPtr->expo == expo)  
					tmpPtr->nextTermPtr = tmp->nextTermPtr->nextTermPtr;
				else
					tmpPtr->nextTermPtr = tmp->nextTermPtr;
				tmp->nextTermPtr = tmpPtr;
				break;
			}
			else if (!tmp->nextTermPtr) {  
				tmp->nextTermPtr = tmpPtr;
				tmpPtr->nextTermPtr = nullptr;
				break;
			}
			tmp = tmp->nextTermPtr;
		}
	}
	return;
}
void addArrayBasedPoly(polynomialTerm a[], polynomialTerm b[], polynomialTerm d[])
{

	int aa = 0, bb = 0, dd = 0;
	while (1) {
		if (a[aa].expo == b[bb].expo) {
			d[dd].expo = a[aa].expo;
			d[dd].coef += a[aa].coef + b[bb].coef;
			if (d[dd].coef == 0)
				dd--;
			aa++, bb++, dd++;
		}
		else if (a[aa].expo > b[bb].expo)
		{
			d[dd].expo = a[aa].expo;
			d[dd].coef += a[aa].coef;
			aa++, dd++;
		}
		else
		{
			d[dd].expo = b[bb].expo;
			d[dd].coef += b[bb].coef;
			dd++, bb++;
		}

		if ((a[aa].coef == 0 && a[aa].expo == 0 && b[bb].coef == 0 && b[bb].expo == 0))
			break;
		if (aa == MAX_TERMS + 1)
			break;
		if (bb == MAX_TERMS + 1)
			break;
	}
}
linkedPolynomialTerm* addLinkBasedPoly(linkedPolynomialTerm* aPtr, linkedPolynomialTerm* bPtr)//////
{
	linkedPolynomialTerm* dPtr = nullptr;

	linkedPolynomialTerm* tmp = dPtr;
	while (aPtr!=0 || bPtr!=0) {
		if ((aPtr && !bPtr) || ((aPtr && bPtr) && aPtr->expo > bPtr->expo)) {
			if (tmp==0) {
				tmp = dPtr = new linkedPolynomialTerm{ aPtr->coef, aPtr->expo };
			}
			else {
				tmp->nextTermPtr = new linkedPolynomialTerm{ aPtr->coef, aPtr->expo };
				tmp = tmp->nextTermPtr;
			}
			aPtr = aPtr->nextTermPtr;
		}
		else if ((aPtr && bPtr) && aPtr->expo == bPtr->expo) {
			if (tmp==0) {
				if (aPtr->coef + bPtr->coef) {
					tmp = dPtr = new linkedPolynomialTerm{ aPtr->coef + bPtr->coef, aPtr->expo };
				}	
			}
			else if (aPtr->coef + bPtr->coef) {
				tmp->nextTermPtr = new linkedPolynomialTerm{ aPtr->coef + bPtr->coef, aPtr->expo };
				tmp = tmp->nextTermPtr;
			}
			aPtr = aPtr->nextTermPtr;
			bPtr = bPtr->nextTermPtr;
		}
		else {
			if (tmp==0) {
				tmp = dPtr = new linkedPolynomialTerm{ bPtr->coef, bPtr->expo };
			}
			else {
				tmp->nextTermPtr = new linkedPolynomialTerm{ bPtr->coef, bPtr->expo };
				tmp = tmp->nextTermPtr;
			}
			bPtr = bPtr->nextTermPtr;
		}
	}
	return dPtr;
}
void printArrayBasedPoly(polynomialTerm terms[])
{
	if (terms[0].coef == 0)
		return;

	if (terms[0].expo == 0)
		cout << terms[0].coef;
	else
		cout << terms[0].coef << "X^" << terms[0].expo;

	for (int i = 1; i < MAX_TERMS; i++) {
		if (terms[i].coef == 0)
			return;

		if (terms[i].expo == 0)
			cout << " + " << terms[i].coef;
		else
			cout << " + " << terms[i].coef << "X^" << terms[i].expo;
	}
}
void printLinkBasedPoly(linkedPolynomialTerm* polyPtr)
{
	linkedPolynomialTerm* termPtr = polyPtr;

	if (termPtr == nullptr)
		return;

	if (termPtr->expo == 0)
		cout << termPtr->coef;
	else
		cout << termPtr->coef << "X^" << termPtr->expo;

	termPtr = termPtr->nextTermPtr;

	while (termPtr != nullptr) {
		if (termPtr->coef == 0)
			break;

		if (termPtr->expo == 0)
			cout << " + " << termPtr->coef;
		else
			cout << " + " << termPtr->coef << "X^" << termPtr->expo;
		termPtr = termPtr->nextTermPtr;
	}
	return;
}
int main()
{
	polynomialTerm a[MAX_TERMS], b[MAX_TERMS], d[MAX_TERMS];
	linkedPolynomialTerm* aPtr, * bPtr, * dPtr;
	int coef, expo;
	aPtr = bPtr = dPtr = nullptr;
	while (1) {
		clear(a); clear(b); clear(d);
		clear(aPtr); clear(bPtr); clear(dPtr);
		for (int i = 0; i < MAX_TERMS; i++) {
			cout << "\ninput a's coefficient and exponent: ";
			cin >> coef >> expo;
			if (expo == 0 && coef == 0)
				break;
			inputTerms(a, coef, expo);
			inputLinkTerms(aPtr, coef, expo);
		}
		cout << "\n\na = ";
		printArrayBasedPoly(a);
		cout << "\na = ";
		printLinkBasedPoly(aPtr);
		cout << "\n";
		for (int i = 0; i < MAX_TERMS; i++) {
			cout << "\ninput b's coefficient and exponent: ";
			cin >> coef >> expo;
			if (expo == 0 && coef == 0)
				break;
			inputTerms(b, coef, expo);
			inputLinkTerms(bPtr, coef, expo);
		}
		cout << "\n\nb = ";
		printArrayBasedPoly(b);
		cout << "\nb = ";
		printLinkBasedPoly(bPtr);
		cout << "\n";
		addArrayBasedPoly(a, b, d);
		cout << "\na + b = ";
		printArrayBasedPoly(d);
		dPtr = addLinkBasedPoly(aPtr, bPtr);
		cout << "\na + b = ";
		printLinkBasedPoly(dPtr);
		cout << "\n";
	}
	return 0;
}
