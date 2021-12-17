# searchin2darray


import java.util.Arrays;
public class Main{
    public static void main(String[] args){
    int[][] arr = {
        {1,3,5,7},
        {10,11,16,20},
        {23,30,34,60}
        //{13,15,16,17}
    };
    System.out.println(Arrays.toString(search(arr,13)));
    }
    public static int[] binSea(int[][] matrix,int row,int cStart,int cEnd,int target){
        while(cStart<=cEnd){
            int mid = cStart + (cEnd - cStart)/2;
            if(matrix[row][mid] == target){
                return new int[] {row,mid};
            }
            if(matrix[row][mid] < target ){
               cStart = mid + 1;
            }
            else{
             cEnd = mid - 1;  
        }
    }
    return new int[] {-1,-1};
    }
    
    public static int[] search(int[][] matrix,int target){
        int row = matrix.length;
        int col = matrix[0].length;
        if(row == 1){
            return binSea(matrix,0,0,col-1,target);
        }
        int rStart = 0;
        int rEnd   = row - 1;
        int cMid   = col / 2;
        while(rStart < (rEnd - 1)){
            int mid = rStart + (rEnd - rStart)/2;
            if (matrix[mid][cMid] == target){
                return new int[] {mid,cMid};
            }
            if(matrix[mid][cMid] < target){
                rStart = mid;
            }
            else{
                rEnd = mid;
            }
        }
        if(matrix[rStart][cMid] == target){
            return new int[] {rStart,cMid};
        }
        if(matrix[rStart + 1][cMid] == target) {
            return new int[] {rStart +1,cMid};
    }
        if(target <= matrix[rStart][cMid-1]){
            return binSea(matrix,rStart,0,cMid-1,target );
        }
        if(target >= matrix[rStart][cMid+1] && target <= matrix[rStart][col-1]){
            return binSea(matrix,rStart,cMid+1,col-1,target );
        }
        if(target <= matrix[rStart + 1][cMid-1]){
            return binSea(matrix,rStart+1,0,cMid-1,target);
        }
        else{
            return binSea(matrix,rStart+1,cMid+1,col-1,target );
        }
    
}}
