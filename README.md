# Meals

Meal planning web app built with Vue.js, with a focus on user experience.

**Note: this project is a work-in-progress and not yet ready for release**

## Why?

All of the meal planning apps I've used in past have had one thing in common: they're slow, clunky, and ugly looking. Every time I try to add a food to my plan, I have to navigate between three different pages -- waiting for each to load -- before seeing the food in my plan. Of course, there have been major improvements towards this particularly in the mobile app department; that's why this app *is not mobile-first*.

I wanted an application that:
- Had a sleek, fast, responsive UI, making it easy to enter new foods and add them to plans
- Focused on calorie and nutrient content of foods, so I can make plans that hit my targets
- Worked on desktop/tablet for traditionally simple data-entry (i.e. mouse/keyboard)

## How?

This app uses the [Vue.js](https://vuejs.org) front-end framework, and was initially built with [Vue CLI](https://cli.vuejs.org).

You may run the application with
`npm run serve`
or build it with
`npm run build`.

## Progress

- [x] Drag & drop foods to meals
- [x] Ability to create new foods
- [ ] Distinction between servings and grams when specifying quantity
- [ ] Food suggestions based on CoFID data
- [ ] Ability to create/change meal names in a meal plan
- [ ] Multiple meal plans
- [ ] Save/loading of meal plans to data store
- [ ] Export meal plans to CSV or equivalent

## License

    Meals: Meal planning web application
    Copyright (C) 2019 David Baxter

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <http://www.gnu.org/licenses/>.