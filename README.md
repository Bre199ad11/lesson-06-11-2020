#include <iostream>
#include <ctime>

using namespace std;

int main() {
	srand(time(0));
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
		}
		cout << endl;
	}

	cout << endl;

	for (int i = 0; i < m; i++) {
		int c = i;
		while (abs(a[c][i]) < 1e-15 && c < m) c++;
		swap(a[c], a[i]);
		for (int j = i + 1; j < m + 1; j++)
			a[i][j] /= a[i][i];
		a[i][i] = 1;
		for (int k = i + 1; k < m; k++) {
			double y = a[k][i];
			for (int j = 0; j < m + 1; j++) {
				a[k][j] -= a[i][j] * y;
			}
		}
	}

	for (int i = 0; i < m; i++) {
		for (int j = 0; j < m + 1; j++) {
			cout << a[i][j] << "\t";
		}
		cout << endl;
	}

	double* x = new double[m];
	for (int i = m - 1; i >= 0; i--) {
		x[i] = a[i][m];
		for (int j = i + 1; j < m; j++) {
			x[i] -= x[j] * a[i][j];
		}
	}
	cout << endl;
	for (int i = 0; i < m; i++) {
		cout << x[i] << "\t";
	}
	cout << endl;
}
