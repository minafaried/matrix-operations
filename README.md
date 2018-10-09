# matrix-operations
// Course:  CS213 - Programming II  - 2018
// Title:   Assignment I - Task 1 - Problem 2
// Program: CS213-2018-A1-T1-P2
// Purpose: Skeleton code for the student to start working
// Author:  Dr. Mohammad El-Ramly
// Date:    10 August 2018
// Version: 1.0
//#include <pch.h>
#include <iostream>
#include <iomanip>
#include <valarray>
#include <cassert>

using namespace std;

// A structure to store a matrix
struct matrix
{
	valarray<int> data;       //valarray that will simulate matrix
	int row, col;
};

// Already implemented
void createMatrix(int row, int col, int num[], matrix& mat);
// Student #1 with the smallest ID (e.g., 20170080)
// All these operations return a new matrix with the calculation result
matrix operator+(matrix mat1, matrix mat2); // Add if same dimensions
matrix operator-  (matrix mat1, matrix mat2); // Sub if same dimensions
matrix operator*  (matrix mat1, matrix mat2); // Multi if col1 == row2
matrix operator+= (matrix& mat1, matrix mat2); // mat1 changes & return
											   // new matrix with the sum
matrix operator-= (matrix& mat1, matrix mat2); // mat1 changes + return new
											   // matrix with difference
void   operator++ (matrix& mat);   	// Add 1 to each element ++mat
void   operator-- (matrix& mat);    	// Sub 1 from each element --mat
istream& operator >> (istream& in, matrix& mat);
ostream& operator<< (ostream& out, matrix mat);
bool   operator== (matrix mat1, matrix mat2);	// True if identical
bool   operator!= (matrix mat1, matrix mat2); 	// True if not same
bool   isSquare(matrix mat);  // True if square matrix
matrix operator+  (matrix mat1, int scalar);  // Add a scalar
matrix operator-  (matrix mat1, int scalar);  // Subtract a scalar
matrix operator*  (matrix mat1, int scalar);  // Multiple by scalar
matrix operator+= (matrix& mat, int scalar);   // change mat & return new matrix
matrix operator-= (matrix& mat, int scalar);   // change mat & return new matrix
matrix transpose(matrix mat);    // Return new matrix with the transpose
bool   isSymetric(matrix mat);  // True if square and symmetric
bool   isIdentity(matrix mat);  // True if square and identity


								//__________________________________________
void cinrow_col(int &row1, int &col1)
{
	cout << "entre the row and the collom of the matrix\n";
	cout << "row  ";
	cin >> row1;
	cout << "\ncol  ";
	cin >> col1;

}
int cin_matrix(int data[], int row1, int col1)
{
	cout << "enter the array of the matrix \n";
	for (int i = 0; i < row1*col1; i++)
	{
		cin >> data[i];
	}
	return *data;
}
void print(matrix mat)
{
	for (int i = 0; i < mat.row*mat.col; i++)
	{
		cout << mat.data[i] << "  ";
	}
}
void choises() {
	cout << "1-Adding Two Matrices \n";
	cout << "2-Subtracting Two Matrices\n";
	cout << "3-Multiplying Two Matrices\n";
	cout << "4-Adding One Matrix To The Main Matrix\n";
	cout << "5-Subtracting One Matrix To The Main Matrix\n";
	cout << "6-Adding 1 to each Element\n";
	cout << "7-Subtracting 1 from each Element\n";
	cout << "8-Check If The Two Matrices Are Equal\n";
	cout << "9-Check If The Two Matrices Aren't Equal\n";
	cout << "10-Chaeck If Square Matrix\n";
	cout << "11-Add Scalar To A Matrix\n";
	cout << "12-Subtract Scalar From A Matrix\n";
	cout << "13-Multiply Scalar To A Matrix\n";
	cout << "14-Add Scalar To Main Matrix\n";
	cout << "15-Subtract Scalar From Main Matrix\n";
	cout << "16-Transpose The Matrix\n";
	cout << "17-Check If Symmetric\n";
	cout << "18-Check If Identitical\n";
}
int main()
{
	int choose;
	choises();
	cin >> choose;
	if (choose == 1)
	{
		int row1, col1, row2, col2;
		cinrow_col(row1, col1);
		cinrow_col(row2, col2);
		if (row1 == row2 && col1 == col2)
		{
			int *data1 = new int[row1*col1];
			int *data2 = new int[row2*col2];
			*data1 = cin_matrix(data1, row1, col1);
			*data2 = cin_matrix(data2, row1, col1);
			matrix mat1;
			matrix mat2;
			createMatrix(row1, col1, data1, mat1);
			createMatrix(row2, col2, data2, mat2);
			matrix addmat;
			addmat.data.resize(mat1.data.size());
			addmat = operator+(mat1, mat2);
			print(addmat);
			delete[]data1;
			delete[]data2;
		}
		else
		{
			cout << "the two matrix can't be add";
		}

	}
	else if (choose == 2)
	{
		int row1, col1, row2, col2;
		cinrow_col(row1, col1);
		cinrow_col(row2, col2);
		if (row1 == row2 && col1 == col2)
		{
			int *data1 = new int[row1*col1];
			int *data2 = new int[row2*col2];
			*data1 = cin_matrix(data1, row1, col1);
			*data2 = cin_matrix(data2, row1, col1);
			matrix mat1;
			matrix mat2;
			createMatrix(row1, col1, data1, mat1);
			createMatrix(row2, col2, data2, mat2);
			matrix submat;
			submat.data.resize(mat1.data.size());
			submat = operator-(mat1, mat2);
			print(submat);
			delete[]data1;
			delete[]data2;
		}
		else
		{
			cout << "the two matrix can't be subtracte";
		}

	}
	else if (choose == 3)
	{
		int row1, col1, row2, col2;
		cinrow_col(row1, col1);
		cinrow_col(row2, col2);
		if (col1 == row2)
		{
			int *data1 = new int[row1*col1];
			int *data2 = new int[row2*col2];
			*data1 = cin_matrix(data1, row1, col1);
			*data2 = cin_matrix(data2, row1, col1);
			matrix mat1;
			matrix mat2;
			createMatrix(row1, col1, data1, mat1);
			createMatrix(row2, col2, data2, mat2);
			matrix  Multiplymat;
			Multiplymat.data.resize(col1*row2);
			Multiplymat = operator*(mat1, mat2);
			print(Multiplymat);
			delete[]data1;
			delete[]data2;
		}
		else
		{
			cout << "the two matrix can't be Multiply";
		}
	}
	else if (choose == 4)
	{
		int row1, col1, row2, col2;
		cinrow_col(row1, col1);
		cinrow_col(row2, col2);
		if (row1 == row2 && col1 == col2)
		{
			int *data1 = new int[row1*col1];
			int *data2 = new int[row2*col2];
			*data1 = cin_matrix(data1, row1, col1);
			*data2 = cin_matrix(data2, row1, col1);
			matrix mat1;
			matrix mat2;
			createMatrix(row1, col1, data1, mat1);
			createMatrix(row2, col2, data2, mat2);
			mat1 = operator+= (mat1, mat2);
			print(mat1);
			delete[]data1;
			delete[]data2;
		}
		else
		{
			cout << "the two matrix can't be add";
		}
	}
	else if (choose == 5)
	{

		int row1, col1, row2, col2;
		cinrow_col(row1, col1);
		cinrow_col(row2, col2);
		if (row1 == row2 && col1 == col2)
		{
			int *data1 = new int[row1*col1];
			int *data2 = new int[row2*col2];
			*data1 = cin_matrix(data1, row1, col1);
			*data2 = cin_matrix(data2, row1, col1);
			matrix mat1;
			matrix mat2;
			createMatrix(row1, col1, data1, mat1);
			createMatrix(row2, col2, data2, mat2);
			mat1 = operator-= (mat1, mat2);
			print(mat1);
			delete[]data1;
			delete[]data2;
		}
		else
		{
			cout << "the two matrix can't be add";
		}
	}
	else if (choose == 6)
	{
		int row, col;
		cinrow_col(row, col);
		int *data = new int[row*col];
		*data = cin_matrix(data, row, col);
		matrix mat;
		createMatrix(row, col, data, mat);
		operator++ (mat);
		print(mat);
	}
	else if (choose == 7)
	{
		int row, col;
		cinrow_col(row, col);
		int *data = new int[row*col];
		*data = cin_matrix(data, row, col);
		matrix mat;
		createMatrix(row, col, data, mat);
		operator-- (mat);
		print(mat);
	}
	else if (choose == 8)
	{
		bool x = true;
		int row1, col1, row2, col2;
		cinrow_col(row1, col1);
		cinrow_col(row2, col2);
		if (row1 == row2 && col1 == col2)
		{
			int *data1 = new int[row1*col1];
			int *data2 = new int[row2*col2];
			*data1 = cin_matrix(data1, row1, col1);
			*data2 = cin_matrix(data2, row1, col1);
			matrix mat1;
			matrix mat2;
			createMatrix(row1, col1, data1, mat1);
			createMatrix(row2, col2, data2, mat2);
			x = operator== (mat1, mat2);
			delete[]data1;
			delete[]data2;
		}
		else
		{
			x = false;
		}
		cout << x;
	}
	else if (choose == 9)
	{
		bool x = false;
		int row1, col1, row2, col2;
		cinrow_col(row1, col1);
		cinrow_col(row2, col2);
		if (row1 == row2 && col1 == col2)
		{
			int *data1 = new int[row1*col1];
			int *data2 = new int[row2*col2];
			*data1 = cin_matrix(data1, row1, col1);
			*data2 = cin_matrix(data2, row1, col1);
			matrix mat1;
			matrix mat2;
			createMatrix(row1, col1, data1, mat1);
			createMatrix(row2, col2, data2, mat2);
			x = operator!= (mat1, mat2);
			delete[]data1;
			delete[]data2;
		}
		else
		{
			x = true;
		}
		cout << x;
	}
	else if (choose == 10)
	{
		int row, col;
		cinrow_col(row, col);
		int *data = new int[row*col];
		*data = cin_matrix(data, row, col);
		matrix mat;
		createMatrix(row, col, data, mat);
		bool x = isSquare(mat);
		cout << x;
	}
	else if (choose == 11)
	{
		int row, col;
		cinrow_col(row, col);
		int *data = new int[row*col];
		*data = cin_matrix(data, row, col);
		matrix mat;
		createMatrix(row, col, data, mat);
		int scalar;
		cout << "\nenter the scalar number\n";
		cin >> scalar;
		matrix scalarmat;
		scalarmat = operator+ (mat, scalar);
		print(scalarmat);
	}
	else if (choose == 12)
	{
		int row, col;
		cinrow_col(row, col);
		int *data = new int[row*col];
		*data = cin_matrix(data, row, col);
		matrix mat;
		createMatrix(row, col, data, mat);
		int scalar;
		cout << "\nenter the scalar number\n";
		cin >> scalar;
		matrix scalarmat;
		scalarmat = operator- (mat, scalar);
		print(scalarmat);
	}
	else if (choose == 13)
	{
		int row, col;
		cinrow_col(row, col);
		int *data = new int[row*col];
		*data = cin_matrix(data, row, col);
		matrix mat;
		createMatrix(row, col, data, mat);
		int scalar;
		cout << "\nenter the scalar number\n";
		cin >> scalar;
		matrix scalarmat;
		scalarmat = operator* (mat, scalar);
		print(scalarmat);
	}
	else if (choose == 14)
	{
		int row, col;
		cinrow_col(row, col);
		int *data = new int[row*col];
		*data = cin_matrix(data, row, col);
		matrix mat1;
		createMatrix(row, col, data, mat1);
		int scalar;
		cout << "\nenter the scalar number\n";
		cin >> scalar;
		matrix scalarmat;
		scalarmat = operator+= (mat1, scalar);
		print(mat1);
	}
	else if (choose == 15)
	{
		int row, col;
		cinrow_col(row, col);
		int *data = new int[row*col];
		*data = cin_matrix(data, row, col);
		matrix mat1;
		createMatrix(row, col, data, mat1);
		int scalar;
		cout << "\nenter the scalar number\n";
		cin >> scalar;
		matrix scalarmat;
		scalarmat = operator-= (mat1, scalar);
		print(mat1);
	}
	else if (choose == 16)
	{
		int row, col;
		cinrow_col(row, col);
		int *data = new int[row*col];
		*data = cin_matrix(data, row, col);
		matrix mat1;
		createMatrix(row, col, data, mat1);
		matrix mattranspose = transpose(mat1);
		print(mattranspose);
	}
	else if (choose == 17)
	{
		int row, col;
		cinrow_col(row, col);
		int *data = new int[row*col];
		*data = cin_matrix(data, row, col);
		matrix mat1;
		createMatrix(row, col, data, mat1);
		bool  Symetric = isSymetric(mat1);
		cout << Symetric;
	}
	else if (choose == 18)
	{
		int row, col;
		cinrow_col(row, col);
		if (row == col)
		{
			int *data = new int[row*col];
			*data = cin_matrix(data, row, col);
			matrix mat1;
			createMatrix(row, col, data, mat1);
			bool  Identity = isIdentity(mat1);
			cout << Identity;
		}
		else
		{
			cout << 0;
		}

	}
	else if (choose == 19) {
	matrix m;
	cin >> m ;
	cout << m ;
	}

	return 0;
}

//__________________________________________
// Takes an array of data and stores in matrix according
// to rows and columns
void createMatrix(int row, int col, int num[], matrix& mat) {
	mat.row = row;
	mat.col = col;
	mat.data.resize(row * col);
	for (int i = 0; i < row * col; i++)
		mat.data[i] = num[i];
}
istream& operator >> (istream& in, matrix& mat) {
	cout << "enter the row and the collom\n";
	cout << "row=>";
	in >> mat.row;
	cout << "\ncollom=>";
	in	>> mat.col;
	mat.data.resize(mat.col*mat.row);
	cout << "\nenter the data of the matrix\n";
	for (int i = 0; i < mat.col*mat.row; i++)
	{
		in >> mat.data[i];
	}
	return in;
}
ostream& operator<< (ostream& out, matrix mat) {
	cout << "the data of the matrix is : ";
	for (int i = 0; i < mat.col*mat.row; i++)
	{
		out << mat.data[i];
	}
	return out;
}

matrix operator+  (matrix mat1, matrix mat2)// Add if same dimensions
{
	matrix a;
	a.col = mat1.col;
	a.row = mat1.row;
	a.data.resize(a.row * a.col);
	for (int i = 0; i < a.row * a.col; i++)
	{
		a.data[i] = mat1.data[i] + mat2.data[i];
	}
	return (a);
}
matrix operator-  (matrix mat1, matrix mat2)// Add if same dimensions
{
	{
		matrix a;
		a.col = mat1.col;
		a.row = mat1.row;
		a.data.resize(a.row * a.col);
		for (int i = 0; i < a.row * a.col; i++)
		{
			a.data[i] = mat1.data[i] - mat2.data[i];
		}
		return (a);
	}
}
matrix operator*  (matrix mat1, matrix mat2)
{
	matrix a;
	a.col = mat2.col;
	a.row = mat1.row;
	a.data.resize(mat1.row*mat2.col);
	int x = 0;
	for (int i = 0; i < mat1.data.size(); i += mat1.col)
	{
		for (int j = 0; j < mat2.data.size() / mat1.col; j++)
		{
			a.data[x] = mat1.data[i] * mat2.data[j] + mat1.data[i + 1] * mat2.data[j + mat1.row];
			x++;
		}
	}
	return a;
}
matrix operator+= (matrix& mat1, matrix mat2)
{
	for (int i = 0; i < mat1.row * mat1.col; i++)
	{
		mat1.data[i] += mat2.data[i];
	}
	return (mat1);
}
matrix operator-= (matrix& mat1, matrix mat2)
{
	for (int i = 0; i < mat1.row * mat1.col; i++)
	{
		mat1.data[i] -= mat2.data[i];
	}
	return (mat1);
}
void   operator++ (matrix& mat)   	// Add 1 to each element ++mat
{
	for (int i = 0; i < mat.row * mat.col; i++)
	{
		mat.data[i] += 1;
	}
}
void   operator-- (matrix& mat)
{
	for (int i = 0; i < mat.row * mat.col; i++)
	{
		mat.data[i] -= 1;
	}
}
bool   operator== (matrix mat1, matrix mat2)
{
	for (int i = 0; i < mat1.row*mat1.col; i++)
	{
		if (mat1.data[i] != mat2.data[i])
		{
			return false;
		}
	}
	return true;
}
bool   operator!= (matrix mat1, matrix mat2)
{
	return !(operator== (mat1, mat2));
}
bool   isSquare(matrix mat)  // True if square matrix
{
	if (mat.col == mat.row)
	{
		return true;
	}
	else
	{
		return false;
	}
}
matrix operator+  (matrix mat1, int scalar)
{
	matrix a;
	a.col = mat1.col;
	a.row = mat1.row;
	a.data.resize(mat1.data.size());
	for (int i = 0; i < mat1.data.size(); i++)
	{
		a.data[i] = mat1.data[i] + scalar;
	}
	return a;
}
matrix operator-  (matrix mat1, int scalar)
{
	matrix a;
	a.col = mat1.col;
	a.row = mat1.row;
	a.data.resize(mat1.data.size());
	for (int i = 0; i < mat1.data.size(); i++)
	{
		a.data[i] = mat1.data[i] - scalar;
	}
	return a;
}
matrix operator*  (matrix mat1, int scalar)
{
	matrix a;
	a.col = mat1.col;
	a.row = mat1.row;
	a.data.resize(mat1.data.size());
	for (int i = 0; i < mat1.data.size(); i++)
	{
		a.data[i] = mat1.data[i] * scalar;
	}
	return a;
}
matrix operator+=  (matrix &mat1, int scalar)
{

	for (int i = 0; i < mat1.data.size(); i++)
	{
		mat1.data[i] += scalar;
	}
	return mat1;
}
matrix operator-=  (matrix &mat1, int scalar)
{

	for (int i = 0; i < mat1.data.size(); i++)
	{
		mat1.data[i] -= scalar;
	}
	return mat1;
}
matrix transpose(matrix mat)
{
	matrix a;
	a.col = mat.col;
	a.row = mat.row;
	a.data.resize(mat.col*mat.row);
	int x = 0;
	for (int i = 0; i < mat.row; i++)
	{
		for (int j = 0; j < mat.data.size(); j += mat.row)
		{
			a.data[x] = mat.data[i + j];
			x++;
		}
	}
	return a;
}
bool   isSymetric(matrix mat)
{
	matrix a = transpose(mat);
	for (int i = 0; i < mat.data.size(); i++)
	{
		if (a.data[i] != mat.data[i])
		{
			return false;
		}
	}
	return true;
}
bool   isIdentity(matrix mat)
{
	for (int i = 0; i < mat.data.size(); i += mat.col + 1)
	{
		if (mat.data[i] != 1)
		{
			return false;
		}
	}
	int  count0 = 0;
	for (int i = 0; i < mat.data.size(); i++)
	{
		if (mat.data[i] == 0)
		{
			count0 += 1;
		}
	}
	if (count0 == 2 && mat.col == 2 || count0 == 6 && mat.col == 3 || count0 == 12 && mat.col == 4)
	{
		return true;
	}
	else
	{
		return false;
	}

}
