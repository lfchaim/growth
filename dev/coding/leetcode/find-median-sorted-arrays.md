``` java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        double ans;
        int sum=0;
        int m=nums1.length;
        int n=nums2.length;
        int[] array1and2 = new int[m + n];
        System.arraycopy(nums1, 0, array1and2, 0, m);
        System.arraycopy(nums2, 0, array1and2, m, n);
        Arrays.sort(array1and2);
        if((m+n)%2==0){
            sum=(m+n)/2;
            ans=(double)(array1and2[sum]+array1and2[sum-1])/2;
        }else{
            sum=(m+n+1)/2;
            ans=array1and2[sum-1];
        }
        return ans;
    }
}
```
## Resultado
Runtime: 4ms Beats 29.99%
Memory: 46.10MB Beats 72.72%

``` java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
		double med = 0;
		int i = 0;
		int j = 0;
		int k = 0;
		int m = nums1.length;
		int n = nums2.length;
		// declare third array - this will contain the merged sorted array 
		int[] nums3 = new int[m+n];
		// merge the given two sorted arrays into the third array
		while(i < m  &&  j < n){
			if (nums1[i] < nums2[j]) {
				nums3[k++] = nums1[i++];
			} 
			else {
				nums3[k++] = nums2[j++];
			}
		}
		/* append any integers that are left */
		while (i < m) {
			nums3[k++] = nums1[i++];
		}
		while (j < n) {
			nums3[k++] = nums2[j++];
		}
		/* now find the median of third array below */
		int len3 = nums3.length;
		// if array length is even
		if(len3 == 0) {
			med = 0;
		}
		else {
			if(len3 % 2 == 0) {
				int n1 = nums3[len3/2 - 1];
				int n2 = nums3[len3/2] ;
				med =  (double)( n1 + n2  ) / 2 ;
			}
		}
		// if array length is odd
		if(len3 % 2 != 0) {
			if(len3 == 1 ) {
				med = nums3[0];
			}
			else {
				med = nums3[len3 / 2 ];
			}
		}
		return med;
    }
}
```

## Resultado
Runtime: 1ms Beats 100.00%
Memory: 45.93MB Beats 84.64%
