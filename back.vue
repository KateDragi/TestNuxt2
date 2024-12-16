<h1 class="show">
    Главная страница (тайтл показывается только на десктопе)
</h1>
<ui-button
    @click="() => {
        useToast(
            'Тестовое уведомление',
        );
    }"
>
    Показать уведомление
</ui-button>
<ui-button
    @click="() => {
        useToast(
            'Тестовое уведомление с ошибкой',
            'destructive',
        )
    }"
>
    Показать уведомление с ошибкой
</ui-button>
<ui-button
    @click="() => {
        userStore.changeName('ЛЕГЕНДА');
    }"
>
    Поменять имя пользователя
</ui-button>

Имя пользователя {{ userStore.name }}

<!-- использование иконок -->
<icons-burger />