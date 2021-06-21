# Matrixx
#include <iostream>
#include <Eigen/Dense>

using namespace std;
using namespace Eigen;

int main()
{
	int n;
	cout << "enter array size n,n: ";
	cin >> n;
	cout << "_________________" << endl;
	
	
	MatrixXd A(n, n);
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			cin >> A(i, j);
		}
	};
	
	cout << "Here is a matrix, A:" << endl << A << endl << endl;

	EigenSolver<MatrixXd> es(A);
	cout << "The eigenvalues of A are:" << endl << es.eigenvalues() << endl;
	cout << "The matrix of eigenvectors, V, is:" << endl << es.eigenvectors() << endl << endl;


	complex<double> lambda = es.eigenvalues()[0];
	cout << "Consider the first eigenvalue, lambda = " << lambda << endl;
	VectorXcd v = es.eigenvectors().col(0);
	cout << "If v is the corresponding eigenvector, then lambda * v = " << endl << lambda * v << endl;
	cout << "... and A * v = " << endl << A.cast<complex<double> >() * v << endl << endl;

	MatrixXcd D = es.eigenvalues().asDiagonal();
	MatrixXcd V = es.eigenvectors();
	cout << "Finally, V * D * V^(-1) = " << endl << V * D * V.inverse() << endl;
}
