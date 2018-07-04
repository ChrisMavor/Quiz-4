# Quiz-4
Christopher Mavor Quiz 04
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

def dot(vector01, vector02):
    """
    This function takes two vectors.
    1) Checks to ensure the lengths are equal.
    2) If not equal, function prints error and returns an empty list.
    3) If equal, the product vector is initialized as en empty list.
    4) Iterates over both vectors
        simulateneously using a range [0,length-1]
    5) During iteration, the value of vector01[i] * vector02[i]
        is stored in the result vector.
    6) Returns product vector.
    """
  
    if(len(vector01) == len(vector02)): #if lengths are equal
        for i in range(len(vector01)): #type validity check
            if ((type(vector01[i]) != int) and (type(vector01[i]) != float) and (type(vector01[i]) != complex)):
                print("Dot ERROR: Invalid Vector01 Type")
                return null
            if ((type(vector02[i]) != int) and (type(vector02[i]) != float) and (type(vector02[i]) != complex)):
                print("Dot ERROR: Invalid Vector02 Type")
                return null
            
        #correct lengths and types
        dotProduct = 0; #initialize product vector
        for i in range(0, len(vector01)): #iterate over range
            dotProduct += (vector01[i] * vector02[i])
        return dotProduct
    
    else: #lengths are not equal.
        print("dot ERROR: Vectors are not of equal length.")
        return null

def scalarVectMultiplication(scalar, vector):
    """
    1) iterate over range [0, length-1]
    2) during iteration, multiply each element vector[i] by scalar;
        store value in vector[i].
    3) return vector
    """
    # type validity check
    for i in range(len(vector)):
        if ((type(vector[i]) != int) and (type(vector[i]) != float) and (type(vector[i]) != complex)):
            print("ScalarVectMult ERROR: Invalid Vector Type")
            return []
    if ((type(scalar) != int) and (type(scalar) != float) and 
        (type(scalar) != complex)):
        print("ScalarVectMult ERROR: Invalid Scalar Type")
        return []
    
    for i in range(0,len(vector)): #iterate over range [0,length-1]
        vector[i] *= scalar; #short-hand
    return vector;

def twoNorm(vector):
    """
    twoNorm takes a vector as it's argument. 
    It then computes the sum of  the squares of each element of the vector. 
    It then returns the square root of this sum.
    """
    # This variable will keep track of the validity of our input.
    inputStatus = True

    # This for loop will check each element of the vector to see if it's a number. 
    for i in range(len(vector)):  
        if ((type(vector[i]) != int) and (type(vector[i]) != float) and (type(vector[i]) != complex)):
            inputStatus = False
            print("Invalid Input")

    # If the input is valid the function continues to compute the 2-norm
    if inputStatus == True:
        result = 0
        # This for loop will compute the sum of the squares of the elements of the vector. 
        for i in range(len(vector)):
            result = result + (vector[i]**2)
        result = result**(1/2)
        return result
    else:
        return null

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
    1) Confirms type validity
    2) Initialize V, Q, R
    3) Copy A into V
    4) Generate R diagonal using twoNorm
    5) Generate Q norm vectors
    6) Complete R upper triangular 
    """
    numCols = len(A[0])
    numRows = len(A)
    
    inputStatus = True
    if (len(A)==0):
      print('ERROR: Empty Matrix')
      inputStatus = False    
    for v in A:
      if (len(v)==0):
       print('ERROR: Empty Vector in Matrix')
       inputStatus = False

    for j in range(numRows):
        for i in range(numCols):
            if ((type(A[j][i]) != int) and (type(A[j][i]) != float) and (type(A[j][i]) != complex)):
                inputStatus = False

    if inputStatus:
        
        V = [[0] * numCols for i in range(numRows)]
        Q = [[0] * numCols for i in range(numRows)]
        R = [[0] * numRows for i in range(numRows)]
        print(A)
        print(R)
        print(Q)
        print(V)

        for i in range(numRows):
            V[i] = A[i]
        
        for i in range(numRows):
            R[i][i] = twoNorm(V[i])
            Q[i] = normalize(V[i])
            
            for j in range(i+1, numRows):
                R[i][j] = dot(Q[i],V[j])
                t = scalarVectMultiplication(R[i][j], Q[i])
                V[j] = vectSubtract(V[j], t)
    
        return [Q,R]
    else:
        return [[],[]]


A = [[6, -11, 6], [0, -6, 0]]

output = QRFactorization(A)

print(output[0])

print(output[1])
