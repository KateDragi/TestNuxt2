<script setup>
import { ref, onMounted } from 'vue';

const root = ref(null);
const slides = ref(null);
const pagination = ref(null);
const prevBtn = ref(null);
const nextBtn = ref(null);

const slider = {
	currentSlide: 0,
	sliderInit(e)
	{
		const styles = window.getComputedStyle(slides.value);
		const left = parseInt(styles.getPropertyValue('left'));
		const slidesCount = slides.value.childElementCount;
		nextBtn.value.style.pointerEvents = 'none';
		prevBtn.value.style.pointerEvents = 'none';

		if (e.target.closest('.slider-block__prev') && left != 0)
		{
			if (left != -750)
			{
				setTimeout(() => prevBtn.value.style.pointerEvents = 'auto', 1000);
			}
			setTimeout(() => nextBtn.value.style.pointerEvents = 'auto', 1000);
			this.slidePrev(slides, left);
		}
		else if (e.target.closest('.slider-block__next') && left != (slidesCount - 1) * -750)
		{
			if (left != (slidesCount - 2) * -750)
			{
				setTimeout(() => nextBtn.value.style.pointerEvents = 'auto', 1000);
			}
			setTimeout(() => prevBtn.value.style.pointerEvents = 'auto', 1000);
			this.slideNext(slides, left);
		}
	},
	paginationGenerator()
	{
		const slidesCount = slides.value.childElementCount;
		for (let index = 0; index < slidesCount; index++)
		{
			const paginationItem = document.createElement('span');
			index == 0 ? paginationItem.className = 'active' : null;
			pagination.value.appendChild(paginationItem);
		}
	},
	slidePrev(slides, left)
	{
		slides.value.style.left = left + 750 + 'px';
		this.currentSlide -= 1;
		this.paginationChange(this.currentSlide, slides);
	},
	slideNext(slides, left)
	{
		slides.value.style.left = left - 750 + 'px';
		this.currentSlide += 1;
		this.paginationChange(this.currentSlide, slides);
	},
	paginationChange(currentSlide)
	{
		for (const element of pagination.value.children)
		{
			element.classList.remove('active');
		}
		pagination.value.children[currentSlide].classList.add('active');
	},
};

onMounted(() =>
{
	slider.paginationGenerator();
});
</script>

<template>
	<div
		ref="root"
		class="main__welcome welcome-block"
	>
		<div
			class="container"
		>
			<div class="welcome-block__grid">
				<div
					class="welcome-block__slider slider-block"
				>
					<div
						ref="slides"
						class="slider-block__slides"
					>
						<div class="slider-block__text">
							<svg
								width="166"
								height="73"
								viewBox="0 0 166 73"
								fill="none"
								xmlns="http://www.w3.org/2000/svg"
							>
								<path
									d="M36.6791 46.3727C46.5705 38.0766 50.0804 32.2269 50.0804 22.3355C50.0804 10.955 44.0179 0 25.1923 0C6.36668 0 0.304199 10.955 0.304199 24.4626H14.1309C14.1309 17.0175 16.3645 13.8267 25.1923 13.8267C34.0201 13.8267 36.2537 16.8048 36.2537 22.3355C36.2537 29.3552 31.3611 33.1841 21.257 41.1611L0.304199 58.4976V72.3243H49.0168V58.4976H22.746L36.6791 46.3727Z"
									fill="#263238"
								/>
								<path
									d="M61.7683 36.5876H102.398V22.7609H61.7683V36.5876ZM61.7683 57.8595H102.398V44.0328H61.7683V57.8595Z"
									fill="#263238"
								/>
								<path
									d="M146 29.7806L163.868 13.8267V0H117.283V13.8267H144.511L128.876 28.717L133.662 39.353H140.895C148.34 39.353 152.169 41.6929 152.169 48.9253C152.169 55.8386 149.191 58.4976 140.044 58.4976C131.003 58.4976 127.919 55.8386 127.919 48.9253H114.092C114.092 61.3693 121.75 72.3243 140.044 72.3243C158.338 72.3243 165.995 61.3693 165.995 49.9889C165.995 35.4177 155.572 28.717 146 29.7806Z"
									fill="#263238"
								/>
							</svg>
							<svg
								width="166"
								height="17"
								viewBox="0 0 166 17"
								fill="none"
								xmlns="http://www.w3.org/2000/svg"
							>
								<path
									d="M3.96932 1.0381H0V16.489H3.96932V10.4233H9.08945V16.489H13.0295V1.0381H9.08945V7.0535H3.96932V1.0381Z"
									fill="#263238"
								/>
								<path
									d="M20.2498 16.7808C22.4636 16.7808 23.8973 15.7849 24.6287 14.3464H24.7457V16.489H28.6858V6.0677C28.6858 2.38603 25.6625 0.836914 22.3271 0.836914C18.7381 0.836914 16.378 2.60733 15.8026 5.42391L19.6451 5.74581C19.9279 4.71977 20.8154 3.96533 22.3076 3.96533C23.7217 3.96533 24.5312 4.69965 24.5312 5.96711V6.02746C24.5312 7.02332 23.5072 7.15409 20.9032 7.41563C17.9384 7.69729 15.2759 8.72333 15.2759 12.1736C15.2759 15.2316 17.3923 16.7808 20.2498 16.7808ZM21.4396 13.8233C20.162 13.8233 19.2453 13.2097 19.2453 12.0328C19.2453 10.8257 20.2108 10.2322 21.6737 10.021C22.5807 9.8902 24.0631 9.6689 24.5604 9.32688V10.9665C24.5604 12.5861 23.2633 13.8233 21.4396 13.8233Z"
									fill="#263238"
								/>
								<path
									d="M37.7161 16.489H45.0891C48.8341 16.489 50.9211 14.9097 50.9211 12.2742C50.9211 10.2423 49.3607 8.6328 46.669 8.43161C48.8146 8.04936 50.0922 6.8825 50.0922 5.21267C50.0922 2.53692 47.8003 1.0381 44.104 1.0381H37.7161V16.489ZM41.5879 13.2802V9.91032H45.0891C46.2399 9.91032 46.9421 10.5843 46.9421 11.6807C46.9421 12.6766 46.2399 13.2802 45.0891 13.2802H41.5879ZM41.5879 7.39552V4.3174H44.104C45.3914 4.3174 46.1814 4.89077 46.1814 5.83634C46.1814 6.81208 45.4304 7.39552 44.1918 7.39552H41.5879Z"
									fill="#263238"
								/>
								<path
									d="M60.0334 16.7908C64.0222 16.7908 66.5287 14.3766 66.7237 10.8257H62.8032C62.5593 12.4754 61.5061 13.4009 60.0822 13.4009C58.1414 13.4009 56.8833 11.721 56.8833 8.76357C56.8833 5.8464 58.1511 4.17657 60.0822 4.17657C61.6036 4.17657 62.5788 5.21267 62.8032 6.75173H66.7237C66.5482 3.18071 63.9247 0.836914 60.0139 0.836914C55.4692 0.836914 52.6604 4.08604 52.6604 8.82392C52.6604 13.5216 55.4204 16.7908 60.0334 16.7908Z"
									fill="#263238"
								/>
								<path
									d="M75.936 16.7908C79.642 16.7908 82.1386 14.9299 82.7238 12.063L78.8813 11.8014C78.4619 12.9784 77.3891 13.592 76.0042 13.592C73.9269 13.592 72.6103 12.1736 72.6103 9.87008V9.86002H82.8116V8.68309C82.8116 3.43219 79.7297 0.836914 75.7702 0.836914C71.362 0.836914 68.5044 4.06592 68.5044 8.83398C68.5044 13.7328 71.323 16.7908 75.936 16.7908ZM72.6103 7.20439C72.6981 5.44403 73.9952 4.03574 75.8384 4.03574C77.6427 4.03574 78.891 5.36356 78.9008 7.20439H72.6103Z"
									fill="#263238"
								/>
								<path
									d="M91.3298 16.489H95.4844V11.0068H97.0351L100.731 16.489H105.666L100.312 8.70321L105.608 1.0381H100.731L96.6547 7.03338H95.4844V1.0381H91.3298V16.489Z"
									fill="#263238"
								/>
								<path
									d="M111.116 1.0381H107.147V16.489H111.116V10.4233H116.236V16.489H120.177V1.0381H116.236V7.0535H111.116V1.0381Z"
									fill="#263238"
								/>
								<path
									d="M127.094 10.8358V1.0381H123.125V16.489H127.251L132.624 6.66119V16.489H136.584V1.0381H132.488L127.094 10.8358Z"
									fill="#263238"
								/>
								<path
									d="M149.899 1.0381H139.64V16.489H143.677V4.40793H149.899V1.0381Z"
									fill="#263238"
								/>
								<path
									d="M156.127 10.8358V1.0381H152.158V16.489H156.283L161.657 6.66119V16.489H165.617V1.0381H161.521L156.127 10.8358Z"
									fill="#263238"
								/>
							</svg>
						</div>
						<div class="slider-block__first-slide" />
						<div class="slider-block__second-slide" />
						<div class="slider-block__third-slide" />
						<div class="slider-block__fourth-slide" />
					</div>
					<div
						ref="prevBtn"
						class="slider-block__prev"
						@click="slider.sliderInit"
					>
						<svg
							width="20"
							height="20"
							viewBox="0 0 20 20"
							fill="none"
							xmlns="http://www.w3.org/2000/svg"
						>
							<path
								fill-rule="evenodd"
								clip-rule="evenodd"
								d="M13.0893 4.41107C12.7639 4.08563 12.2362 4.08563 11.9108 4.41107L6.91079 9.41107C6.58535 9.73651 6.58535 10.2641 6.91079 10.5896L11.9108 15.5896C12.2362 15.915 12.7639 15.915 13.0893 15.5896C13.4147 15.2641 13.4147 14.7365 13.0893 14.4111L8.67855 10.0003L13.0893 5.58958C13.4147 5.26414 13.4147 4.73651 13.0893 4.41107Z"
								fill="#2A3D48"
								fill-opacity="0.5"
							/>
						</svg>
					</div>
					<div
						ref="nextBtn"
						class="slider-block__next"
						@click="slider.sliderInit"
					>
						<svg
							width="20"
							height="20"
							viewBox="0 0 20 20"
							fill="none"
							xmlns="http://www.w3.org/2000/svg"
						>
							<path
								fill-rule="evenodd"
								clip-rule="evenodd"
								d="M13.0893 4.41107C12.7639 4.08563 12.2362 4.08563 11.9108 4.41107L6.91079 9.41107C6.58535 9.73651 6.58535 10.2641 6.91079 10.5896L11.9108 15.5896C12.2362 15.915 12.7639 15.915 13.0893 15.5896C13.4147 15.2641 13.4147 14.7365 13.0893 14.4111L8.67855 10.0003L13.0893 5.58958C13.4147 5.26414 13.4147 4.73651 13.0893 4.41107Z"
								fill="#2A3D48"
								fill-opacity="0.5"
							/>
						</svg>
					</div>
					<div
						ref="pagination"
						class="slider-block__pagination"
					/>
				</div>
				<div class="welcome-block__book-of-the-day book-item book-item--day-book">
					<div class="book-item__top">
						<h3 class="book-item__book-of-title">
							Книга дня
						</h3>
						<div class="book-item__time">
							08:56:31
						</div>
					</div>
					<div class="book-item__suggest" />
					<div class="book-item__image">
						<a href="#">
							<img
								src="/public/oleg.png"
								alt="Фото женщины"
							>
						</a>
					</div>
					<div class="book-item__category">
						<a href="#">Корпоративное право</a>
					</div>
					<h4 class="book-item__title">
						<a href="#">Инвестирование: способы, риски, субъекты : монография</a>
					</h4>
					<div class="book-item__author">
						<a href="#">Майфат А.В.</a>
					</div>
					<div class="book-item__price">
						4 450 ₽
					</div>
					<div class="book-item__bottom">
						<button class="book-item__cart">
							<svg
								width="20"
								height="20"
								viewBox="0 0 20 20"
								fill="none"
								xmlns="http://www.w3.org/2000/svg"
							>
								<path
									fill-rule="evenodd"
									clip-rule="evenodd"
									d="M2.49996 2.5C2.03972 2.5 1.66663 2.8731 1.66663 3.33333C1.66663 3.79357 2.03972 4.16667 2.49996 4.16667V3.33333L2.49997 4.16667H2.5H2.50014H2.50024H2.50036H2.5005H2.50067H2.50155H2.50277H2.50351H2.50391H2.50434H2.50624H2.50848H2.50909H2.50972H2.51105H2.54309H2.66272H3.07288H3.50144L5.43735 12.6847C5.53716 13.1239 5.96689 13.4025 6.40583 13.3186C6.45656 13.3283 6.50892 13.3333 6.56246 13.3333H15C15.3473 13.3333 15.6583 13.1179 15.7802 12.7926L18.2802 6.12594C18.3762 5.87002 18.3406 5.58332 18.1849 5.35867C18.0292 5.13403 17.7733 5 17.5 5H5.4L4.97924 3.14865C4.89301 2.76924 4.55571 2.5 4.16663 2.5H3.07288H2.66272H2.54309H2.538H2.53322H2.53207H2.53094H2.52874H2.52456H2.51717H2.51633H2.51551H2.51472H2.51394H2.51319H2.51246H2.51105H2.50624H2.50434H2.50391H2.50351H2.50277H2.50067H2.50036H2.50024H2.50014H2.5H2.49997L2.49996 3.33333V2.5ZM5.77879 6.66667L6.91515 11.6667H14.4225L16.2975 6.66667H5.77879ZM8.33329 14.1667C7.41282 14.1667 6.66663 14.9129 6.66663 15.8333C6.66663 16.7538 7.41282 17.5 8.33329 17.5C9.25377 17.5 9.99996 16.7538 9.99996 15.8333C9.99996 14.9129 9.25377 14.1667 8.33329 14.1667ZM11.6666 15.8333C11.6666 14.9129 12.4128 14.1667 13.3333 14.1667C14.2538 14.1667 15 14.9129 15 15.8333C15 16.7538 14.2538 17.5 13.3333 17.5C12.4128 17.5 11.6666 16.7538 11.6666 15.8333Z"
									fill="#FF7A00"
								/>
							</svg>
							<span>В корзину</span>
						</button>
						<button class="book-item__favorite">
							<svg
								width="20"
								height="20"
								viewBox="0 0 20 20"
								fill="none"
								xmlns="http://www.w3.org/2000/svg"
							>
								<path
									fill-rule="evenodd"
									clip-rule="evenodd"
									d="M6.66667 4.1818C6.66667 3.71884 7.03976 3.34353 7.5 3.34353H12.5C12.9602 3.34353 13.3333 3.71884 13.3333 4.1818V16.2339C13.3333 16.5967 12.9061 16.7882 12.6379 16.5454L10.5575 14.6619C10.2405 14.375 9.75945 14.375 9.44253 14.6619L7.36207 16.5454C7.09393 16.7882 6.66667 16.5967 6.66667 16.2339V4.1818ZM7.5 1.66699H12.5C13.8807 1.66699 15 2.79291 15 4.1818V16.2339C15 18.0482 12.8637 19.0053 11.523 17.7916L10 16.4128L8.47701 17.7916C7.13633 19.0053 5 18.0482 5 16.2339V4.1818C5 2.79291 6.11929 1.66699 7.5 1.66699Z"
									fill="#1C294D"
									fill-opacity="0.5"
								/>
							</svg>
						</button>
					</div>
				</div>
				<div class="welcome-block__advertisement-first advertisement-block advertisement-block--first">
					<div class="advertisement-block__text">
						<span>Бесплатно доставим ваш заказ при покупке от 2000 ₽</span>
						<svg
							width="126"
							height="31"
							viewBox="0 0 126 31"
							fill="none"
							xmlns="http://www.w3.org/2000/svg"
						>
							<path
								d="M5 21C42 4.5 102.5 24.5 117.5 7"
								stroke="#FF7A00"
								stroke-width="20"
							/>
						</svg>
					</div>
					<div class="advertisement-block__image">
						<img
							src="../public/delivery.svg"
							alt="Картинка доставщика"
						>
					</div>
				</div>
				<div class="welcome-block__advertisement-second advertisement-block advertisement-block--second">
					<div class="advertisement-block__text">
						<span>Скидка при регистрации до 15%</span>
						<svg
							width="67"
							height="28"
							viewBox="0 0 67 28"
							fill="none"
							xmlns="http://www.w3.org/2000/svg"
						>
							<path
								d="M7.5 20.5C27.5 0.5 40.5 27 60 8"
								stroke="#79ECC1"
								stroke-width="20"
							/>
						</svg>
					</div>
					<div class="advertisement-block__image">
						<img
							src="../public/discount.svg"
							alt="Картинка человека"
						>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<style>

</style>
