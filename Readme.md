# PPT - DSA Assignment 19

## Answer 1:
```js
const merge = (list1, list2) => {
    if (list1 == null)
        return list2;
    if (list2 == null)
        return list1;

    if (list1.val < list2.val) {
        list1.next = merge(list1.next, list2);
        return list1;
    } else {
        list2.next = merge(list1, list2.next);
        return list2;
    }
};

const mergeKLists = (lists) => {
    let answerList = null;

    for (let i = 0; i < lists.length; i++) {
        answerList = merge(answerList, lists[i]);
    }

    return answerList;

};
```

<br/>

## Answer 2:
```js
Array.prototype.bisect_left = function (target) {
    let start = 0;
    let end = this.length - 1;
    let mid = 0;

    while (this[mid] !== target) {
        mid = (start + end) >> 1;

        if (this[mid] > target)
            end = mid - 1;
        else if (this[mid] < target)
            start = mid + 1;
    }
    while (this[mid] === this[mid - 1])
        mid--;

    return mid;
}


/**
 * @param {number[]} nums
 * @return {number[]}
 */

const countSmaller = nums => {

    let arr = [...nums].sort((a, b) => a - b);
    let ans = [];
    
    //console.log({ length: nums.length });
    if (nums.length > 999)
        for (let i = 0; i < nums.length; i++) {
            ans[i] = arr.bisect_left(nums[i]);
            arr.splice(ans[i], 1);
        }
    else
        for (let i = 0; i < nums.length; i++) {
            ans[i] = arr.indexOf(nums[i]);
            arr.splice(ans[i], 1);
        }
    return ans;
};
```

<br/>

## Answer 3:
```js
const sortArray = nums => {
    let sorted;

    do {
        sorted = false;
        for (let i = 0; i <= nums.length; i++) {
           
            if (nums[i] > nums[i + 1]) {
                let temp = nums[i + 1];
                nums[i + 1] = nums[i];
                nums[i] = temp;
                sorted = true;
            }
        }
    } while (sorted);
    return nums;
};
```

<br/>

## Answer 4:
```js
const moveAllZeroes = (nums) => {
    for (let i = nums.length - 1; i >= 0; i--) {

        //if zero is found at any place - splice it and push a zero into the array
        if (nums[i] === 0) {
            nums.push(0);
            nums.splice(i, 1);
        }
    }
    return nums;
};
```

<br/>

## Answer 5:
```js
const rearrangeArray = nums => {
    let positiveNums = nums.filter(x => x > 0);
    let negativeNums = nums.filter(x => x < 0);
    let result = [];

    for (let i = 0; i < nums.length / 2; i++) {
        result.push(positiveNums[i], negativeNums[i]);
    }

    return result;
};
```

<br/>

## Answer 6:
```js
const mergeArrays = (nums1, nums2) => {
    let m = nums1.length;
    let n = nums2.length;
    // let nums3;
    for (let i = m, j = 0; j < n; i++, j++) {
        nums1[i] = nums2[j];
    }
    return nums1.sort((a, b) => a - b);
};
```

<br/>

## Answer 7:
```js
const intersectionOfArrays = (nums1, nums2) => {
    let arr = [];
    let obj = {};
    for (let i = 0; i < nums1.length; i++) {
        if (obj[nums1[i]] == undefined) {
            obj[nums1[i]] = 1;
        }
    }
    // console.log(obj)

    for (let i = 0; i < nums2.length; i++) {
        if (obj[nums2[i]] == 1) {
            arr.push(nums2[i]);

            obj[nums2[i]] = 0;

        }
    }
    return arr;
};
```

<br/>

## Answer 8:
```js
const intersectArrays = (nums1, nums2) => {
    const map1 = nums1.reduce((acc, num) => ({
        ...acc,
        [num]: (acc[num] ?? 0) + 1,
    }), {});
    const map2 = nums2.reduce((acc, num) => ({
        ...acc,
        [num]: (acc[num] ?? 0) + 1,
    }), {});

    return Object.keys(map1).flatMap((num) => {
        const count = Math.min(map1[num], map2[num] ?? 0);
        return Array(count).fill(num);
    });
};
```