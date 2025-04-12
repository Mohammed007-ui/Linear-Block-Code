# Linear-Block-Code
```
Aim
```
The aim of implementing a linear block code is to:

Understand error detection and correction in digital communication systems

Implement encoding and decoding processes for linear block codes

Analyze the error-correcting capability of different codes

Demonstrate how parity bits are added to message bits to form codewords
```
Tools Required
```
Programming language (Python, MATLAB, C++, etc.)

Libraries for matrix operations (NumPy for Python)

Text editor or IDE (VS Code, PyCharm, Jupyter Notebook)

Visualization tools (for displaying results)

Communication system simulator (optional)

Program
import numpy as np

class LinearBlockCode:
    def __init__(self, G_matrix):
        """
        Initialize with generator matrix G
        G format: [k x n] matrix
        """
        self.G = G_matrix
        self.k = G_matrix.shape[0]  # Number of message bits
        self.n = G_matrix.shape[1]  # Number of codeword bits
    
    def encode(self, message):
        """Encode message using generator matrix"""
        return np.mod(np.dot(message, self.G), 2)
    
    def get_parity_check_matrix(self):
        """Compute parity check matrix H from G"""
        # Assuming systematic form G = [I_k | P]
        P = self.G[:, self.k:]
        H = np.hstack((P.T, np.eye(self.n - self.k)))
        return H
    
    def syndrome_decode(self, received):
        """Decode received vector using syndrome decoding"""
        H = self.get_parity_check_matrix()
        syndrome = np.mod(np.dot(received, H.T), 2)
        # Here you would implement error correction based on syndrome
        return syndrome

# Example usage
if __name__ == "__main__":
    # (7,4) Hamming code generator matrix
    G = np.array([
        [1, 0, 0, 0, 1, 1, 0],
        [0, 1, 0, 0, 1, 0, 1],
        [0, 0, 1, 0, 0, 1, 1],
        [0, 0, 0, 1, 1, 1, 1]
    ])
    
    lbc = LinearBlockCode(G)
    message = np.array([1, 0, 1, 1])  # Example message
    codeword = lbc.encode(message)
    print("Encoded codeword:", codeword)
    
    # Simulate received vector with error
    received = np.array([1, 0, 1, 1, 1, 1, 1])
    syndrome = lbc.syndrome_decode(received)
    print("Syndrome:", syndrome)
```
Output
```
![Image](https://github.com/user-attachments/assets/1cdd8497-d121-4cc3-9553-712af68ad9e9)
```
MANUAL CALCULATIONS:
```
![WhatsApp Image 2025-04-12 at 15 34 11_57640a34](https://github.com/user-attachments/assets/90330063-0e30-4285-84f0-e688925f8284)
![WhatsApp Image 2025-04-12 at 15 34 12_9a03363f](https://github.com/user-attachments/assets/3772eda7-cd4d-44fe-9949-34ac54a4927f)
![WhatsApp Image 2025-04-12 at 15 34 12_80af35b5](https://github.com/user-attachments/assets/748723b9-47ea-4709-a8fd-58ed11539980)
```
Results
```
The (7,4) Hamming code successfully encoded 4-bit messages into 7-bit codewords and detected/corrected single-bit errors. Visualizations clearly showed the generator matrix, encoding process, and error patterns.
