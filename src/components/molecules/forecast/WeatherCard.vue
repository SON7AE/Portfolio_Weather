<template>
    <div class="weather-card">
        <div class="weather-card__button-box">
            <BasicButton :label="'시간대별 날씨 정보'" />
            <BasicButton :label="'이번 주 날씨 보기'" :data-theme="'forecast'" />
        </div>
        <div class="weather-card__info-box">
            <ForecastTimelyWeather v-for="(data, index) in aTimelyWeatherDatas" :key="index" :data="data" :icon="aTimelyWeatherIcons[index]" class="weather-card__info-box__timely-weather" />
        </div>
    </div>
</template>

<script>
import BasicButton from '~/components/atoms/BasicButton.vue';
import ForecastTimelyWeather from '~/components/molecules/forecast/TimelyWeather.vue';

import { storeToRefs } from 'pinia';
import { useStore } from '~/store/index';

export default {
    components: { BasicButton, ForecastTimelyWeather },
    setup() {
        const store = useStore();
        const { aTimelyWeatherDatas, aTimelyWeatherIcons } = storeToRefs(store);

        return { aTimelyWeatherDatas, aTimelyWeatherIcons };
    },
};
</script>

<style lang="scss" scoped>
@import '~/assets/styles/main.scss';

.weather-card {
    display: flex;
    flex-direction: column;
    align-items: center;

    width: 100%;
    margin-top: 12px;

    &__button-box {
        display: flex;
        align-items: center;
        justify-content: space-between;

        width: 100%;
        gap: 48px;
    }
    &__info-box {
        display: flex;
        align-items: center;
        justify-content: space-between;

        max-width: 280px;

        padding: 8px;
        gap: 12px;

        overflow: scroll;

        &__timely-weather {
            &:first-child {
                background-color: $color-blue-000;
            }
        }
    }
}
</style>
