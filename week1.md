# Some JS Array methods you probably never use!🧐🤔

Hello, devs 🤗. Welcome to our first series on the exploration of powerful JavaScript array methods. These methods can significantly improve your code efficiency and readability in real-world web projects.

*I know you wanna demonstrate your JS prowess with those custom functions you're writing but these might really save you some time when building🧏.
Also, all examples here are framework agnostic, meaning they are not based on any frameworks or tools, just pure / vanilla JS. Frameworks and tools come and go but the foundation remains the same!*


## 1. Array.from()

`Array.from()` creates a new Array instance from an array-like or iterable object.

### Practical Examples

Converting a NodeList to an Array:
```javascript
const paragraphs = document.querySelectorAll('p');
const paragraphArray = Array.from(paragraphs);
paragraphArray.forEach(p => p.classList.add('highlight'));
```

Creating an array of objects from form inputs:
```javascript
const form = document.querySelector('form');
const inputs = form.querySelectorAll('input[type="text"]');
const inputData = Array.from(inputs, input => ({ name: input.name, value: input.value }));
console.log(inputData);
```

## 2. Array.prototype.reduce()

The `reduce()` method executes a reducer function on each element of the array, resulting in a single output value.

### Practical Examples

Calculating total price in a shopping cart:
```javascript
const cart = [
  { name: 'T-Shirt', price: 15.99, quantity: 2 },
  { name: 'Jeans', price: 39.99, quantity: 1 },
  { name: 'Shoes', price: 59.99, quantity: 1 }
];

const total = cart.reduce((acc, item) => acc + (item.price * item.quantity), 0);
console.log(`Total: NGN${total.toFixed(2)}`); // Total: NGN115.97
```

Grouping blog posts by category:
```javascript
const posts = [
  { id: 1, category: 'JavaScript', title: 'Array Methods' },
  { id: 2, category: 'CSS', title: 'Flexbox Guide' },
  { id: 3, category: 'JavaScript', title: 'ES6 Features' }
];

const groupedPosts = posts.reduce((acc, post) => {
  acc[post.category] = acc[post.category] || [];
  acc[post.category].push(post);
  return acc;
}, {});

console.log(groupedPosts); // Output: { JavaScript: [...], CSS: [...] }
```

## 3. Array.prototype.some()

The `some()` method tests whether at least one element in the array passes the test implemented by the provided function.

### Practical Examples

Checking if any checkbox in a form is checked:
```javascript
const checkboxes = document.querySelectorAll('input[type="checkbox"]');
const isAnyChecked = Array.from(checkboxes).some(checkbox => checkbox.checked);
console.log(`Form can be submitted: ${isAnyChecked}`);
```

Validating if any field in a form is empty:
```javascript
const formInputs = document.querySelectorAll('.form-input');
const hasEmptyField = Array.from(formInputs).some(input => input.value.trim() === '');
console.log(`Form has empty fields: ${hasEmptyField}`);
```

## 4. Array.prototype.every()

The `every()` method tests whether all elements in the array pass the test implemented by the provided function.

### Practical Examples

Checking if all required fields in a form are filled:
```javascript
const requiredInputs = document.querySelectorAll('.required');
const allFieldsFilled = Array.from(requiredInputs).every(input => input.value.trim() !== '');
console.log(`All required fields are filled: ${allFieldsFilled}`);
```

Verifying if all items in a todo list are completed:
```javascript
const todoItems = [
  { id: 1, text: 'Learn JavaScript', completed: true },
  { id: 2, text: 'Build a project', completed: true },
  { id: 3, text: 'Deploy to production', completed: false }
];

const allCompleted = todoItems.every(item => item.completed);
console.log(`All todos completed: ${allCompleted}`);
```

## 5. Array.prototype.flatMap()

The `flatMap()` method first maps each element using a mapping function, then flattens the result into a new array.

### Practical Examples

Extracting and flattening tags from blog posts:
```javascript
const blogPosts = [
  { id: 1, title: 'JavaScript Basics', tags: ['javascript', 'programming'] },
  { id: 2, title: 'CSS Layouts', tags: ['css', 'design'] },
  { id: 3, title: 'React Hooks', tags: ['javascript', 'react', 'hooks'] }
];

const allTags = blogPosts.flatMap(post => post.tags);
console.log(`All tags: ${allTags}`);
```

Creating a flat list of comments and replies:
```javascript
const comments = [
  { id: 1, text: 'Great article!', replies: ['Thanks!', 'Glad you enjoyed it'] },
  { id: 2, text: 'Looking forward to more', replies: [] },
  { id: 3, text: 'Could you elaborate on point 3?', replies: ['Sure, I'll update the post'] }
];

const allComments = comments.flatMap(comment => [comment.text, ...comment.replies]);
console.log(allComments);
```

## 6. Array.prototype.at()

The `at()` method takes an integer value and returns the item at that index, allowing for positive and negative integers.

### Practical Examples

Accessing the last element in a breadcrumb trail:
```javascript
const breadcrumbs = ['Home', 'Products', 'Electronics', 'Smartphones'];
const currentPage = breadcrumbs.at(-1);
console.log(`You are here: ${currentPage}`); // Output: "You are here: Smartphones"
```

Implementing a carousel that loops infinitely:
```javascript
// Separate state to keep track of the current index
let currentIndex = 0;

// Wrapper Function to create the next function
function createNext(items) {
  return function next() {
    currentIndex = (currentIndex + 1) % items.length; 
    return items.at(currentIndex);
  };
}

// Wrapper function to create the previous function 
function createPrevious(items) {
  return function previous() {
    currentIndex = (currentIndex - 1 + items.length) % items.length;
    return items.at(currentIndex);
  };
}

// Wrapper function to create the currentItem function
function createCurrentItem(items) {
  return function currentItem() {
    return items.at(currentIndex);
  };
}

// Test the code
const items = ['Image1', 'Image2', 'Image3', 'Image4', 'Image5'];
const next = createNext(items);
const previous = createPrevious(items);
const currentItem = createCurrentItem(items);

console.log(currentItem());  // 'Image1'
console.log(next());         // 'Image2'
console.log(next());         // 'Image3'
console.log(next());         // 'Image4'
console.log(previous());     // 'Image3'
console.log(currentItem());  // 'Image3'


```

Thanks for reading, builders 🙇. Look out for some code challenges to practice implementation of some of these methods soon! 😉
