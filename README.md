# Quiz-4
# Christopher Mavor Quiz 04
def scalarVectMultiplication(scalar, vector):
    """
    Input: Scalar and a vector
    Iterate over range [length]. During iteration, multiply each element vector[i] by scalar and stores value in vector[i].
    Output: return vector
    """
    # type validity check
    for i in range(len(vector)):
        if ((type(vector[i]) != int) and (type(vector[i]) != float) and (type(vector[i]) != complex)):
            eturn ("Invalid Vector") #invalid input
    if ((type(scalar) != int) and (type(scalar) != float) and 
        (type(scalar) != complex)):
        return ("Invalid Scalar") #invalid input
    
    for i in range(len(vector)): #iterate over range [length-1]
        vector[i] *= scalar; 
    return vector;

def dot(vector01, vector02):
    """
    Input: two vectors.
    Checks to ensure the lengths are equal. If not equal, function prints error and returns an empty list. If equal, the product vector is initialized as en empty list. Iterates over both vectors simulateneously using a range [length-1]
    
    Output: Returns the dot product of the vectors.
    """
  
    if(len(vector01) == len(vector02)): #if lengths are equal
        for i in range(len(vector01)): #type validity check
            if ((type(vector01[i]) != int) and (type(vector01[i]) != float) and (type(vector01[i]) != complex)):
                return ("Invalid Vector01 Type") #invalid input
            if ((type(vector02[i]) != int) and (type(vector02[i]) != float) and (type(vector02[i]) != complex)):
                return ("Invalid Vector02 Type") #invalid input
            
        #correct lengths and types
        dotProduct = 0; #initialize product vector
        for i in range(0, len(vector01)): #iterate over range
            dotProduct += (vector01[i] * vector02[i])
        return dotProduct
    
    else: #lengths are not equal.
        return ("Invalid Vector Types") #invalid inputs
def vectSubtract(vector01, vector02):
    """
    Checks that inputs are number and are the same length.
    If vectors are not compatable then error returned
    """
    
    if(len(vector01) == len(vector02)): #checking vector length
      vectSubtract = [] #initialize subtraction vector
      for i in range(0, len(vector01)): #iterate over range
        vectSubtract.append(vector01[i] - vector02[i]) #compute and append vector elements to end of subtraction vector.
        return vectSubtract

    else:
      return ["VectSub ERROR: Vectors are not of equal length."]



def twoNorm(vector):
    """
    Input: A single Vector
    
    Output: Computes the sum of the squares of each element of the vector and then returns the square root of this sum.
    """
#Check to see if input vector is valid for problem
    for i in range(len(vector)):  
        if ((type(vector[i]) != int) and (type(vector[i]) != float) and (type(vector[i]) != complex)):
            inputStatus = False
            print("Invalid Input")
    # If the input is valid the function continues to compute the 2-norm
        else:
            result = 0
            # This for loop will compute the sum of the squares of the elements of the vector. 
            for i in range(len(vector)):
                result = result + (vector[i]**2)
            result = result**(1/2)
            return result

def normalize(vector) :
    """
    1) check if empty vector.
    2) If empty, print Error and return null.
    3) If not empty vector, 
    4) compute and store infNorm in infNorm
    5) Iterate over range [0, len-1]
    6) during iteration
        compute element / infNorm store in current vector index.
    """
    
    if (len(vector) == 0):
        print("ERROR: Empty Vector")
        return []
    for i in range(len(vector)):
            if ((type(vector[i]) != int) and (type(vector[i]) != float) and (type(vector[i]) != complex)):
                print("Normalize ERROR: Invalid Vector Type")
                return []
    else:
        tNorm = twoNorm(vector)
        for i in range(len(vector)):
            vector[i] *= (1/tNorm)
        return vector

def QRFactorization(A):
    """
    QRFactorization takes a matrix as it's argument
    Output: V diagonal using twoNorm. Q norm vectors. R upper triangular 
    """
    Cols = len(A[0])
    Rows = len(A)
    
    inputStatus = True
    if (len(A)==0):
      print('ERROR: Empty Matrix')
      inputStatus = False    
    for v in A:
      if (len(v)==0):
       print('ERROR: Empty Vector in Matrix')
       inputStatus = False

    for j in range(Rows):
        for i in range(Cols):
            if ((type(A[j][i]) != int) and (type(A[j][i]) != float) and (type(A[j][i]) != complex)):
                inputStatus = False

    if inputStatus == True:
        
        V = [[0] * Cols for i in range(Rows)]
        Q = [[0] * Cols for i in range(Rows)]
        R = [[0] * Rows for i in range(Rows)]
        print(A)
        print(R)
        print(Q)
        print(V)

        for i in range(Rows):
            V[i] = A[i]
        
        for i in range(Rows):
            R[i][i] = twoNorm(V[i])
            Q[i] = normalize(V[i])
            
            for j in range(i+1, Rows):
                R[i][j] = dot(Q[i],V[j])
                t = scalarVectMultiplication(R[i][j], Q[i])
                V[j] = vectSubtract(V[j], t)
    
        return [Q,R]
    else:
        return [[],[]]


A = [[2, -11, 63], [9, -6, 40]]

output = QRFactorization(A)

print(output[0])

print(output[1])
