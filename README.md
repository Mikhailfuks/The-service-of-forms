// Функция для создания элемента формы
function createFormElement(type, label, name, options = []) {
 const element = document.createElement(type);
 element.classList.add('form-element');

 if (label) {
  const labelElement = document.createElement('label');
  labelElement.textContent = label;
  labelElement.htmlFor = name;
  element.appendChild(labelElement);
 }

 if (type === 'select') {
  options.forEach(option => {
   const optionElement = document.createElement('option');
   optionElement.value = option.value;
   optionElement.textContent = option.text;
   element.appendChild(optionElement);
  });
 } else {
  element.type = type;
  element.name = name;
 }

 return element;
}

// Функция для создания формы
function createForm(formElements) {
 const form = document.createElement('form');
 form.classList.add('form');

 formElements.forEach(element => {
  form.appendChild(element);
 });

 // Добавление кнопки отправки
 const submitButton = document.createElement('button');
 submitButton.type = 'submit';
 submitButton.textContent = 'Отправить';
 form.appendChild(submitButton);

 return form;
}

// Пример использования:
// Создание элементов формы
const nameInput = createFormElement('input', 'Имя', 'name');
const emailInput = createFormElement('input', 'Email', 'email');
const messageTextarea = createFormElement('textarea', 'Сообщение', 'message');
const genderSelect = createFormElement('select', 'Пол', 'gender', [
 { value: 'male', text: 'Мужской' },
 { value: 'female', text: 'Женский' },
]);

// Создание формы
const form = createForm([nameInput, emailInput, messageTextarea, genderSelect]);

// Добавление формы на страницу
document.body.appendChild(form);

// Обработка отправки формы
form.addEventListener('submit', (event) => {
 event.preventDefault(); // Отменяем стандартную отправку
 // Получаем значения из формы
 const formData = new FormData(event.target);
 // Обрабатываем данные формы (отправка на сервер, обработка на стороне клиента)
 console.log(formData); // Вывод значений в консоль для демонстрации
});
