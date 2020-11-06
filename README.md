#include <iostream>
using namespace std;
int main() {
	int m = 5;
	double** a = new double*[m];
	for (int i = 0; i < m; i++) {
		a[i] = new double[m + 1];
	}
	

	for (int i = 0; i < m; i++) {
		for (int j = 0; j < m; j++) {
			a[i][j] = rand() % 21 - 10;
		}
		a[i][m] = rand() % 201 - 100;
	}
	for (int i = 0; i < m; i++) {
		for (int j = 0; j < m + 1; j++) {
			cout << a[i][j] << "\t";
		}cout << endl;
	}cout << endl;
	


	for (int i = 0; i < m; i++) {
		int k = i; 
		while (a[k][i] == 0 && k<m) k++;
		swap(a[k], a[i]);
		for (int j = i + 1; j < m; j++) {
			a[i][j] / a[i][i];
		}
		a[i][i] = 1;
		for (int k = i + 1; i < m; i++) {
			double y = a[k][i];
			for (int j = 0; j < m; j++) {
				a[k][j] -= a[i][j] * y;
			}
		}
	}
	double* x = new double[m];
	for (int i = m - 1; i >= 0; i--) {
		x[i] = a[i][m];
		for (int j = i + 1; j < m; j++) {
			x[i] -= x[j] * a[i][j];
		}
	}
	for (int i = 0; i < m; i++) {
		cout << x[i] << "\t";

	}
	cout << endl;
}
