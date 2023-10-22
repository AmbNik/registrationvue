<template>
    <div>
        <form @submit.prevent="checkForm">
<!--            <p v-if="errors.length">-->
<!--                <b>Пожалуйста, исправьте следующие ошибки:</b>-->
<!--            <ul>-->
<!--                <li v-for="error in errors" :key="error">{{ error }}</li>-->
<!--            </ul>-->
<!--            </p>-->

            <p>
                <label for="email">*Почта:</label>
                <input  @input="validateEmail"  type="text" name="email" id="email"  v-model="email" placeholder="Введите почту" />
            <p class="error-message" v-if="emailError">{{ emailError }}</p>
            </p>

            <p class="password-input relative-position">
                <label for="password">*Пароль:</label>
                <input v-model="password" :type="showPassword ? 'text' : 'password'" placeholder="Пароль" />
                <span class="password-icon" @click="togglePasswordVisibility">&#x1F441;</span>
            <p  class="error-message"  v-if="passwordError">{{ passwordError }}</p>
            </p>

            <p class="password-input relative-position">
                <label for="ConfirmPassword">*Повтор пароля:</label>
                <input v-model="confirmPassword" :type="showConfirmPassword ? 'text' : 'password'" placeholder="Повтор пароля" />
                <span class="password-icon" @click="toggleConfirmPasswordVisibility">&#x1F441;</span>
                            <p class="error-message"  v-if="confirmPasswordError">{{ confirmPasswordError }}</p>
            </p>

            <p>
                <label for="phone">*Телефон:</label>
                <input  type="text" name="phone" id="phone" v-model="phone" placeholder="Введите номер телефона" />
                            <p  class="error-message"  v-if="phoneError">{{ phoneError }}</p>
            </p>

            <p>
                <label for="surname">*Фамилия:</label>
                <input type="text" name="surname" id="surname" v-model="surname" placeholder="Введите фамилию" />
                            <p  class="error-message"  v-if="surnameError">{{ surnameError }}</p>
            </p>

            <p>
                <label for="firstName">*Имя:</label>
                <input type="text" name="firstName" id="firstName" v-model="firstName" placeholder="Введите имя" />
                            <p class="error-message"  v-if="firstNameError">{{ firstNameError }}</p>
            </p>

            <p>
                <label for="patronymic">*Отчество:</label>
                <input type="text" name="patronymic" id="patronymic" v-model="patronymic" placeholder="Введите отчество" />
                             <p class="error-message"  v-if="patronymicError">{{ patronymicError }}</p>
            </p>









            <p>
                <label for="movie">Типы услуг</label>
                <select name="movie" id="movie" v-model="movie" >
                    <option>Ремонт квартир</option>
                    <option>Ремонт офисов</option>
                    <option>Дизайн интерьера</option>
                    <option>Реставрация помещений</option>
                    <option>Отделка помещений</option>
                </select>
            </p>

            <p>
                <label for="wishes">Ваши пожелания:</label>
                <input type="text" name="wishes" id="wishes" v-model="wishes" placeholder="Введите ваши пожелания" />
                <span class="tooltip-icon" @mouseover="handleTooltipShow" @mouseout="handleTooltipHide">⚠️</span>
                <span class="tooltip" v-show="showTooltip">Расскажите, какой ремонт вы планируете</span>
            </p>

            <p>
                <label>Выберите виды работ, которые вас интересуют:</label>
            </p>
            <div class="checkbox-group">
                <div class="checkbox-row">
                    <input type="checkbox" id="painting" v-model="painting" value="Покраска и обои"/>
                    <label for="painting">Покраска и обои</label>
                </div>
                <div class="checkbox-row">
                    <input type="checkbox" id="tiles" v-model="tiles" value="Плитка и полы" />
                    <label for="tiles">Плитка и полы</label>
                </div>
                <div class="checkbox-row">
                    <input type="checkbox" id="construction" v-model="construction" value="Строительство и перепланировка" />
                    <label for="construction">Строительство и перепланировка</label>
                </div>
                <div class="checkbox-row">
                    <input type="checkbox" id="electricity" v-model="electricity" value="Электрика и освещение" />
                    <label for="electricity">Электрика и освещение</label>
                </div>
            </div>

            <p>
                <label>Какой стиль интерьера вас интересует?</label>
            </p>



            <div class="radio-group">
                <div class="radio-row">
                    <input type="radio" id="modern" value="Современный" v-model="interiorStyle" />
                    <label for="modern">Современный</label>
                </div>
                <div class="radio-row">
                    <input type="radio" id="classic" value="Классический" v-model="interiorStyle" />
                    <label for="classic">Классический</label>
                </div>
                <div class="radio-row">
                    <input type="radio" id="eclectic" value="Эклектика" v-model="interiorStyle" />
                    <label for="eclectic">Эклектика</label>
                </div>
                <div class="radio-row">
                    <input type="radio" id="minimalism" value="Минимализм" v-model="interiorStyle" />
                    <label for="minimalism">Минимализм</label>
                </div>
            </div>

            <p>
                <label for="photo">Фотография:</label>
                <input type="file" name="photo" id="photo" accept="image/*" @change="handleFileUpload" />
            <p class="error-message"  v-if="uploadedFileError">{{ uploadedFileError }}</p>
            </p>

            <div class="checkbox-row">
                <div class="checkbox-wrapper">
                    <input type="checkbox" id="agreement" v-model="agreement" />
                    <label for="agreement">Я прочитал и согласен с условиями использования сайта, включая политику конфиденциальности и правила обработки персональных данных</label>
                </div>
            </div>

            <p>
                <button type="submit" :disabled="isFormValid">Отправить</button>
            </p>
            <router-link to="/Login">Уже есть аккаунт? Войти</router-link>

<!--            <h3>Данные в хранилище:</h3>-->
<!--            <span>Фамилия: {{ register.surname }}</span><br>-->
<!--            <span>Имя: {{ register.firstName }}</span><br>-->
<!--            <span>Отчество: {{ register.patronymic }}</span><br>-->
<!--            <span>Почта: {{ register.email }}</span><br>-->
<!--            <span>Типы услуг: {{ register.movie }}</span><br>-->
<!--            <span>Пароль: {{ register.password }}</span><br>-->
<!--            <span>Повтор пароля: {{ register.confirmPassword }}</span><br>-->
<!--            <span>Телефон: {{ register.phone }}</span><br>-->
<!--            <span>Ваши пожелания: {{ register.wishes }}</span><br>-->
<!--            <span>Файл: {{ register.uploadedFile }}</span><br>-->
<!--            <h4>Выберите виды работ, которые вас интересуют:</h4>-->
<!--            <span>Строительство и перепланировка: {{ register.construction }}</span><br>-->
<!--            <span>Покраска и обои: {{ register.painting }}</span><br>-->
<!--            <span>Плитка и полы: {{ register.tiles }}</span><br>-->
<!--            <span>Электрика и освещение: {{ register.electricity }}</span><br>-->

<!--            <h4>Выберите виды работ, которые вас интересуют:</h4>-->
<!--            <span>{{ register.interiorStyle }}</span><br>-->






        </form>
    </div>
</template>

<script>
import {computed, inject, ref, toRefs, watch} from 'vue';
import { mask } from 'vue-the-mask';
import  { useRegisterStore } from '../stores/RegisterStore';
import { useRouter } from 'vue-router';


export default {
    directives: {
        mask
    },
    setup() {
        const router = useRouter();
        const register = useRegisterStore();
        const isFormValid = computed(() => {
            return (
                !email.value ||
                !password.value ||
                !confirmPassword.value ||
                !phone.value ||
                !surname.value ||
                !firstName.value ||
                !patronymic.value ||
                !agreement.value ||
                emailError.value !== '' ||
                passwordError.value !== '' ||
                confirmPasswordError.value !== '' ||
                phoneError.value !== '' ||
                surnameError.value !== '' ||
                firstNameError.value !== '' ||
                patronymicError.value !== ''||
                uploadedFileError.value !==''
            );
        });


        const agreement = ref(false);
        const uploadedFile = ref(null);
        const email = ref('');
        const movie = ref('');
        const errors = ref([]);
        const password = ref('');
        const confirmPassword = ref('');
        const showPassword = ref(false);
        const showConfirmPassword = ref(false);
        const surname = ref('');
        const firstName = ref('');
        const patronymic = ref('');
        const phone = ref('');
        const wishes = ref('');
        const showTooltip = ref(false);
        const interiorStyle = ref('');
        const painting =  ref(false);
        const tiles =  ref(false);
        const construction =  ref(false);
        const electricity =  ref(false);


        const emailError = ref('');
        const passwordError = ref('');
        const confirmPasswordError = ref('');
        const phoneError = ref('');
        const surnameError = ref('');
        const firstNameError = ref('');
        const patronymicError = ref('');
        const uploadedFileError = ref('');



        // Функция валидации email
        const validateEmail = () => {
            errors.value = [];

            if (!email.value) {
                emailError.value = 'Введите вашу электронную почту.';
            } else if (!email.value.match(/^[^\s@]+@[^\s@]+\.[^\s@]+$/)) {
                emailError.value = 'Введите корректный адрес электронной почты.';
            } else {
                emailError.value = ''; // Очистка сообщения об ошибке, если валидация успешна
            }
        };

        // Прослушивание изменений в поле email и запуск функции валидации
        watch(email, () => {
            validateEmail();
        });


        // Функция валидации пароля

        const validatePassword = () => {
            errors.value = []; // Сброс ошибок перед проверкой

            if (!password.value) {
                passwordError.value = 'Введите пароль.';
            } else if (password.value.length < 8) {
                passwordError.value = 'Пароль должен содержать не менее 8 символов.';
            } else if (!/[A-Z]/.test(password.value) && !/[А-Я]/.test(password.value)) {
                passwordError.value = 'Пароль должен содержать хотя бы одну заглавную букву.';
            } else if (!/[a-z]/.test(password.value) && !/[а-я]/.test(password.value)) {
                passwordError.value = 'Пароль должен содержать хотя бы одну строчную букву.';
            } else if (!/\d/.test(password.value)) {
                passwordError.value = 'Пароль должен содержать хотя бы одну цифру.';
            } else if (!/[!@#$%^&*(),.?":{}|<>]/.test(password.value)) {
                passwordError.value = 'Пароль должен содержать хотя бы один специальный символ(!@#$%^&*(),.?":{}|<>).';
            } else if (confirmPassword.value !== '' && confirmPassword.value !== password.value) {
                passwordError.value = 'Пароли не совпадают.';
            } else {
                passwordError.value = ''; // Очистка сообщения об ошибке, если валидация успешна
            }
        };

        // Прослушивание изменений в поле пароля и запуск функции валидации
        watch(password,validatePassword);

        // Функция валидации повторного пароля
        const validateConfirmPassword = () => {
            errors.value = []; // Сброс ошибок перед проверкой

            if (!confirmPassword.value) {
                confirmPasswordError.value = 'Введите повторный пароль.';
            } else if (confirmPassword.value !== password.value) {
                confirmPasswordError.value = 'Пароли не совпадают.';
            } else if (!password.value) {
                confirmPasswordError.value = 'Введите пароль.';
            } else {
                confirmPasswordError.value = ''; // Очистка всех сообщений об ошибке, если валидация успешна
            }
        };


        // Прослушивание изменений в поле повторного пароля и запуск функции валидации
        watch(confirmPassword, validateConfirmPassword
        );


        // Функция валидации телефона
        const validatePhone = () => {
            errors.value = []; // Сброс ошибок перед проверкой

            if (!phone.value) {
                phoneError.value = 'Введите ваш номер телефона.';
            } else {
                const phoneRegex = /^\+7\d{10}$/;
                if (!phoneRegex.test(phone.value)) {
                    phoneError.value = 'Введите корректный номер телефона в формате +7 (999) 999-9999.';
                } else {
                    phoneError.value = ''; // Очистка сообщения об ошибке, если валидация успешна
                }
            }
        };

        // Прослушивание изменений в поле телефона и запуск функции валидации
        watch(phone, () => {
            validatePhone();
        });

        // Функция валидации фамилии
        const validateSurname = () => {
            errors.value = []; // Сброс ошибок перед проверкой

            if (!surname.value) {
                surnameError.value = 'Введите вашу фамилию.';
            } else if (surname.value.length < 2 || surname.value.length > 50) {
                surnameError.value = 'Минимум 2 символа и максимум 50 символов.';
            } else if (/\d/.test(surname.value)) {
                surnameError.value = 'Фамилия не должна содержать цифры.';
            } else {
                surnameError.value = ''; // Очистка сообщения об ошибке, если валидация успешна
            }
        };


        // Прослушивание изменений в поле фамилии и запуск функции валидации
        watch(surname, () => {
            validateSurname();
        });

        // Функция валидации имени
        const validateFirstName = () => {
            errors.value = []; // Сброс ошибок перед проверкой

            if (!firstName.value) {
                firstNameError.value = 'Введите ваше имя.';
            } else if (firstName.value.length < 2 || firstName.value.length > 50) {
                firstNameError.value = 'Минимум 2 символа и максимум 50 символов.';
            } else if (/\d/.test(firstName.value)) {
                firstNameError.value = 'Имя не должно содержать цифры.';
            } else {
                firstNameError.value = ''; // Очистка сообщения об ошибке, если валидация успешна
            }
        };


        // Прослушивание изменений в поле имени и запуск функции валидации
        watch(firstName, () => {
            validateFirstName();
        });

        // Функция валидации отчества
        const validatePatronymic = () => {
            errors.value = []; // Сброс ошибок перед проверкой

            if (!patronymic.value) {
                patronymicError.value = 'Введите ваше отчество.';
            } else if (patronymic.value.length < 2 || patronymic.value.length > 50) {
                patronymicError.value = 'Минимум 2 символа и максимум 50 символов.';
            } else if (/\d/.test(patronymic.value)) {
                patronymicError.value = 'Отчество не должно содержать цифры.';
            } else {
                patronymicError.value = ''; // Очистка сообщения об ошибке, если валидация успешна
            }
        };


        // Прослушивание изменений в поле отчества и запуск функции валидации
        watch(patronymic, () => {
            validatePatronymic();
        });




        const checkForm = (event) => {


            // Установите значения полей формы в хранилище
            // register.setUploadedFile(uploadedFile.value);
            register.setEmail(email.value);
            register.setPassword(password.value);
            register.setConfirmPassword(confirmPassword.value);
            register.setPhone(phone.value);
            register.setSurname(surname.value);
            register.setFirstName(firstName.value);
            register.setPatronymic(patronymic.value);
            register.setMovie(movie.value);
            register.setWishes(wishes.value);
            register.setInteriorStyle(interiorStyle.value);
            register.setPainting(painting.value);
            register.setTiles(tiles.value);
            register.setConstruction(construction.value);
            register.setElectricity(electricity.value);
            register.setAgreement(agreement.value);


            // Если проверки прошли успешно, выполните отправку данных формы
            // Например, отправьте запрос на сервер с данными формы
            console.log('Данные отправлены:', {
                surname: surname.value,
                firstName: firstName.value,
                patronymic: patronymic.value,
                email: email.value,
                movie: movie.value,
                phone: phone.value, // Добавили номер телефона к данным для отправки
                password: password.value,
                confirmPassword: confirmPassword.value
            });

            // Очистите поля формы после отправки
            surname.value = '';
            firstName.value = '';
            patronymic.value = '';
            email.value = '';
            movie.value = '';
            password.value = '';
            confirmPassword.value = '';
            showPassword.value = false;
            phone.value = '';
            wishes.value ='';
            interiorStyle.value = '';
            painting.value = false;
            tiles.value = false;
            construction.value = false;
            electricity.value = false;
            agreement.value = false;
            emailError.value = '';
            passwordError.value = '' ;
            confirmPasswordError.value = '' ;
            phoneError.value = '' ;
            surnameError.value = '' ;
            firstNameError.value = '' ;
            patronymicError.value = '';
            // Перенаправьте пользователя на другую страницу
            router.push('/');

            // Проверьте uploadedFile на наличие файла перед отправкой формы
            //         if (!uploadedFile.value) {
            //             errors.value.push('Загрузите фотографию.');
            //         }
            // Другие проверки...
            // if (!email.value) {
            //     errors.value.push('Введите вашу электронную почту.');
            // }
            // if (!surname.value) {
            //     errors.value.push('Введите вашу фамилию.');
            // }
            //
            // if (!firstName.value) {
            //     errors.value.push('Введите ваше имя.');
            // }
            //
            // if (!patronymic.value) {
            //     errors.value.push('Введите ваше отчество.');
            // }
            // if (!agreement.value) {
            //     errors.value.push('Согласитесь с условием');
            // }
            // Другие проверки...
        };

        const togglePasswordVisibility = () => {
            showPassword.value = !showPassword.value;
        };

        const toggleConfirmPasswordVisibility = () => {
            showConfirmPassword.value = !showConfirmPassword.value;
        };

        const handleTooltipShow = () => {
            showTooltip.value = true;
        };

        const handleTooltipHide = () => {
            showTooltip.value = false;
        };

        const handleFileUpload = (event) => {
            const file = event.target.files[0];

            // Проверяем формат файла
            const allowedFormats = ['image/png', 'image/jpeg', 'image/gif', 'image/bmp'];
            if (file && !allowedFormats.includes(file.type)) {
                uploadedFileError.value = 'Формат файла должен быть PNG, JPEG, GIF или BMP.';
            } else {
                uploadedFileError.value = ''; // Очистка сообщения об ошибке, если валидация успешна

                // Если формат файла допустимый, сохраняем его в FormData и передаем в хранилище
                const formData = new FormData();
                formData.append('photo', file); // 'photo' - это имя поля файла, которое ожидается на бэкенде
                // Сохраняем объект FormData в хранилище
                register.setUploadedFile(formData);
            }
        };





        return {
            surname,
            firstName,
            patronymic,
            email,
            movie,
            errors,
            checkForm,
            password,
            confirmPassword,
            showPassword,
            showConfirmPassword,
            togglePasswordVisibility,
            toggleConfirmPasswordVisibility,
            phone, // Добавили переменную для хранения номера телефона
            wishes,
            showTooltip,
            handleTooltipShow,
            handleTooltipHide,
            interiorStyle,
            uploadedFile,
            handleFileUpload,
            agreement,
            painting,
            tiles,
            construction,
            electricity,
            isFormValid,
            register,
            validateEmail,
            validateConfirmPassword,
            validatePassword,
            validatePhone,
            validateSurname,
            validateFirstName,
            validatePatronymic,
            emailError,
            passwordError,
            confirmPasswordError,
            phoneError,
            surnameError,
            firstNameError,
            patronymicError,
            uploadedFileError,



        };
    },
};
</script>

<style scoped>
/* Стили для формы */
form {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
}

p {
    margin-bottom: 15px;
}

label {
    display: block;
    margin-bottom: 5px;
}

.checkbox-group {
    display: flex;
    flex-wrap: wrap;
    border: 1px solid #ccc; /* Толщина, стиль и цвет рамки */
    padding: 10px; /* Добавление внутренних отступов для рамки */
    border-radius: 5px; /* Закругление углов рамки */
}

.checkbox-row {
    flex: 0 0 50%; /* Две колонки */
    margin-bottom: 10px;
}




.radio-row {
    display: flex; /* Размещаем элементы в ряд */
    align-items: center; /* Выравниваем элементы по вертикали по центру */
    margin-bottom: 10px;
}
.checkbox-wrapper {
    display: flex;
    align-items: center;
}

.checkbox-wrapper input {
    margin-right: 10px; /* Расстояние между чекбоксом и текстом */
}

.error-message {
    color: red; /* Устанавливаем красный цвет для текста ошибки */
}
</style>

