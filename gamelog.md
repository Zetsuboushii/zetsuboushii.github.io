---
layout: home
title: Gamelog
permalink: /gamelog/
header: true
category: game
---

<div class="sunken-panel" style="width: 379px">
    <table>
        <thead>
        <tr>
            <th>Title</th>
            <th>Platform</th>
            <th>Last Played</th>
            <th>Rating</th>
        </tr>
        </thead>
        <tbody>
        {% assign games_posts = site.entries | sort: "lastplayed" | reverse %}
        {% for post in games_posts %}
            {% if post.category == "game" %}
                <tr>
                    <td>{{ post.title }}</td>
                    <td>{{ post.platform }}</td>
                    <td>{{ post.lastplayed | date: "%d.%m.%Y" }}</td>
                    <td>
                        {% for i in (1..5) %}
                            {% if i <= post.rating %}
                                ★
                            {% else %}
                                ☆
                            {% endif %}
                        {% endfor %}
                    </td>
                </tr>
            {% endif %}
        {% endfor %}
        </tbody>
    </table>
</div>

<menu role="tablist" id="tablist" style="margin-top: 20px">
    {% assign game_posts = site.entries | where: "category", "game" %}
    {% assign sorted_posts = game_posts | sort: "lastplayed" %}
    {% assign grouped_posts = sorted_posts | group_by_exp: "post", "post.lastplayed | date: '%Y-%m'" %}

    {% for group in grouped_posts %}
        <li role="tab" aria-selected="{{ forloop.last }}" data-tab="{{ group.name }}">
            {{ group.name | date: "%B %Y" }}
        </li>
    {% endfor %}
</menu>
<div class="window tabpanel-container">
    {% for group in grouped_posts %}
        <div id="{{ group.name }}" class="window-body tabpanel" role="tabpanel"
             aria-hidden="{% if forloop.last %}false{% else %}true{% endif %}">
            {% for post in group.items %}
                <fieldset>
                    <legend>{{ post.title }}</legend>
                    <p>
                        <b>Plattform:</b> {{ post.platform }} /
                        <b>Bewertung:</b> {% for i in (1..5) %}{% if i <= post.rating %}★{% else %}☆{% endif %}{% endfor %}
                    </p>
                    {% assign filename = post.path | split: '/' | last %}
                    {% assign basename = filename | split: '.' | first %}
                    <img src="{{ "/assets/imgs/games/" | relative_url }}{{ basename }}.png" alt=""
                         style="max-width: 616px; max-height: 300px">
                    {{ post.content }}
                </fieldset>
            {% endfor %}
        </div>
    {% endfor %}
</div>

<script>
    document.addEventListener("DOMContentLoaded", () => {
        const tabs = document.querySelectorAll('[role="tab"]');
        const panels = document.querySelectorAll('.tabpanel');

        tabs.forEach((tab) => {
            tab.addEventListener("click", () => {
                tabs.forEach((t) => t.setAttribute("aria-selected", "false"));
                panels.forEach((p) => p.setAttribute("aria-hidden", "true"));

                tab.setAttribute("aria-selected", "true");
                const tabId = tab.getAttribute("data-tab");
                document.getElementById(tabId).setAttribute("aria-hidden", "false");
            });
        });
    });
</script>